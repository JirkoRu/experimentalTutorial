# An experimental Tutorial with a bandit task

*"I think the connection of the predictions made by your model to cognition/neuroscience is not as strong as implied by your introduction and discussion..."*

Maybe you have gotten a comment like this before. This practical will hopefully some basic insight into what might be involved in human data collection and maybe next time you can refer reviewer 2 to your cool behavioural results that qualitatively match your model predictions.

In this practical we will build a bandit task that can nicely run in your browser. I hope this tutorial will give some insight into what might be involved in human data collection. Who knows, maybe you might even want contact me in the future to run your own quick human experiment on prolific. 

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
For this tutorial we will use psychex, which was developed in Chris Summerfield's lab (my co-advisor), but there are many alternatives out there that all have their pros and cons.

Now you can open the project in your favourite code editor. and open `js/main.js`. This file holds the code for the tutorial. Normally we might want to separate things into different modules but for simplicity it is all there. 

You will see three important functions. Ignore their content for now. Here is what they are doing:

- `preload()` This function is responsible for loading static content before the rest of the display renders. Static content refers to external content that’s delivered to the user unchanged, for example: Images, Fonts, Gifs.

- `setup()` This function should contain any code that needs to be run once, before any rendering happens. Think of this as a sort of init method.

- `draw()` This function is an animation loop: it extends the JS requestAnimationFrame() function. This function is run many times per second, typically based on the display refresh rate: e.g., for a 60Hz display, draw() will run 60 times per second.

There is many more relevant details but for this tutorial we will leave it here. We can now start to fill in elements of our task which is currently quite sad looking.

### 3. Working on a bandit task
Let's fill in the blanks!

1. *Change the icon of the slot machines.* You can find the relevant lines in the constructor of the slotmachine task
Currently our arms are just represented as boring buttons and nothing happens. In `preload()` we are loading a slot machine image. We would like to use it instead. For this we have the `pImage(x,y, image)` class which takes three arguments. can you replace the button with the image? <details><summary>**SPOILER**</summary>
something like: `new pImage(25 + i*40, 50, assets.imgs.slotMachine)`
</details>

2. show the payout in the console. 

3. set the probability of payout!
At the bottom of the file you can find a `BanditTask` class. You can see how it is instantiate in `setup()` 
```gameContent.myBanditTask = new BanditTask(0, 0, 2, [0.5, 0.5]);```
It currently takes four inputs (x,y, nArms, probs). The x and y coordinates are currently useless and an artifact of the inheritance structure. Go ahead and change the payout probability of the two arms to something more exciting.
4. show the payout on screen.
5. Add a timer.
6. Make a selection for the better bandit.

