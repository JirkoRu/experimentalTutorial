# An experimental Tutorial with a bandit task

*"I think the connection of the predictions made by your model to cognition/neuroscience is not as strong as implied by your introduction and discussion..."*

Maybe you have gotten a comment like this before. This practical will hopefully some basic insight into what might be involved in human data collection and maybe next time you can refer reviewer 2 to your cool behavioural results that qualitatively match your model predictions.

In this practical we will build a bandit task that can run in your browser. I hope this tutorial will give some insight into what might be involved in human data collection. Who knows, maybe you might even want contact me in the future to run your own quick human experiment on prolific. 

Many credits to [Alex Grogan](https://github.com/agrogan97) who is responsible for psychex and some components of this tutorial. 

## Step-by-Step tutorial

### 1. Basic Setup
First clone this repo with `git clone https://github.com/JirkoRu/experimentalTutorial.git`. Then navigate to the project folder and in the project root i.e., `experimentalTutorial/` and run 
```
python -m http.server
```

Then you should be able to navigate to http://127.0.0.1:8000 in your browser to see the project. 

Currently, it is not much of a task, but we will progressively add elements to make it into a somewhat proper two armed bandit task. 

### 2. The basics of Psychex 
For this tutorial we will use psychex, but there are many alternatives out there that all have their pros and cons.

Now you can open the project in your favourite code editor. and open `js/main.js`. This file holds the code for the tutorial. Normally we might want to separate things into different modules but for simplicity it is all there. 

You will see three important functions. Ignore their content for now. Here is what they are doing:

- `preload()` This function is responsible for loading static content before the rest of the display renders. Static content refers to external content that’s delivered to the user unchanged, for example: Images, Fonts, Gifs.

- `setup()` This function should contain any code that needs to be run once, before any rendering happens. Think of this as a sort of init method.

- `draw()` This function is an animation loop: it extends the JS requestAnimationFrame() function. This function is run many times per second, typically based on the display refresh rate: e.g., for a 60Hz display, draw() will run 60 times per second.

There is many more relevant details but for this tutorial we will leave it here. We can now start to fill in elements of our task which is currently quite sad looking.

### 3. We are gonna coda a bandit task
Let's fill in the blanks!

1. *Change the icon of the slot machines.* 

    Currently our arms are just represented as boring buttons and nothing happens. In `preload()` we are loading a slot machine image. We would like to use it instead. We need to replace the Button in the constructor of the `BanditTask` class.  with For this we have the `pImage(x,y, image)` class which takes three arguments. can you replace the button with the image? Refresh your browser to see any changes.<details><summary>SPOILER</summary>
    something like: `new pImage(25 + i*50, 50, assets.imgs.slotMachine)` should work.
    </details>

2. *Show the result of the draws in the console.*

    Now that we have changed the icon you should be seeing the cute slot machine icons instead of the boring old buttons. Next we would like to have some real onClick functionality that shows us if we get a payout or not. We need to use javascript's `console.log()` to print things in the console. Navigate to your browser settings and open the developer tools. Then click the console tab. 

    Next you can see that we have an `onClick` function in the `BanditTask` constructor which defines what happens if the element is clicked. `e.id` will contain the id of the arm and `result` contains the outcome of this pull of the arm. Try to log to the console what happens on each draw.
    <details><summary>SPOILER</summary>
    console.log(`${e.id} pulled ${result}`)
    </details>


3. *Set the probability of payout!*

    At the bottom of the file you can find a `BanditTask` class. You can see how it is instantiate in `setup()` 
    ```gameContent.myBanditTask = new BanditTask(0, 0, 2, [0.5, 0.5]);```
    It currently takes four inputs (x,y, nArms, probs). The x and y coordinates are currently useless and an artifact of the inheritance structure. Go ahead and change the payout probability of the two arms to something more exciting. 

4. *Show the payout on screen.*

    Next we actually wanna show the payout on screen. Let's go ahead and do that. First let's update the overall payout the player has achieved.
    ```
    if (result) {
        this.score += 1;
    }
    this.resultText.setText(`Score: ${this.score}`)
    ```
    Can you find where this code needs to go?
    <details><summary>SPOILER</summary>
    The onClick function in the BanditTask is the right place.
    </details>
    Next lets highlight on screen whenever each arm pays out. We need to draw the outcome. 

    ```
    if (e.id == "arm1"){
        result ? this.textA.setText("Score +1") : this.textA.setText("No Score")
    } else if (e.id == "arm2"){
        result ? this.textB.setText("Score +1") : this.textB.setText("No Score")
    }
    ```

    After we have updated it we want to remove it after a short period of time.

    ```
    setTimeout(() => {
    e.id == "arm1" ? this.textA.setText("") : this.textB.setText("");
    }, 1500)
    ```
    Again you can find the place where this code should go. 
    <details><summary>SPOILER</summary>
    The onClick function in the BanditTask is the right place.
    </details>

### Bonus tasks
5. *Make a selection for the better bandit.* 

    Here is the [psychex documentation](https://agrogan97.github.io/psychex/tutorial/getting_started.html) to help you with this. 
    Currently the "end game" button leads us to something questionable. Ideally we might want to have a selection screen afterwards that allows us to choose the better bandit. Can you make it happen?

6. *Add a timer that counts down to decision* 

    In a more real task we might want people to have limited time to sample with a subsequent decision about which arm is more valuable. [Here](https://agrogan97.github.io/psychex/code_docs/primitives.html#Countdown) is a link to a countdown object that would allow you to implement something like this. The definition of the Countdown class is in line 1212 of `lib/psychex/psychex.maint.js`of this repo if you want to look at the code.


7. *Datasaving*

8. *Hosting the experiment*
