# An experimental Tutorial with a bandit task

Many credits to [Alex Grogan](https://github.com/agrogan97) who developed psychex and the basic components of this tutorial. 

## Step-by-Step tutorial

### 1. Basic Setup
First clone this repo with `git clone https://github.com/JirkoRu/experimentalTutorial.git`. Then navigate to the project folder and in the project root i.e., `experimentalTutorial/` and run 
```
python -m http.server
```

Then you should be able to navigate to http://127.0.0.1:8000 in your browser to see the project.

### 2. The basics of Psychex 
Now you can open the project in your favourite code editor. and open `js/main.js`. This file holds the code for the tutorial. Normally we might want to separate things into different modules but for simplicity it is all there. 

You will see three important functions. Ignore their content for now. I will explain what they are doing 

- `preload()` loads static content in advance.

- `setup()` contains code to be run once at the start of the experiment

- `draw()` contains renderable content that can be run many times per second according to your refresh rate.

### 3. Working on a bandit task
Now fill the blanks.
1. set the probability of payout.
2. Change the icon of the bandits.
3. show the payout in the console.
4. show the payout on screen.
5. Add a timer.
6. Make a selection for the better bandit.

