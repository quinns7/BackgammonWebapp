# CS 347 Final Project

## Contributors 

Sophie Quinn, Hannah Scooler, Selma Vangstein, Bryan Yang 

## Short Description
We built this application over the course of 7 weeks using Golang, PostgreSQL, HTML, CSS and Javascript. The app is built with the hope of giving the user a smooth and joyful Backgammon experience. 

## How to Use 
Our app should hopefully be easy to use. Follow these steps and you should be in for a joyful experience!
(numbers here will be fixed when I am sure we are done with adding things)
1. Clone the repo
2. Download Docker if you don't have it, and make sure you have the docker engine running
3. Run 'docker compose build' and 'docker compose up'
4. Follow the link to localhost:9000 to get to the home page
5. Follow your heart! Hopefully it is intuitive to use but if you'd like some more guidance, keep reading... 

6. Here, you can choose to freshen up on the game rules, register a new account, or go straight to new game to play as a guest
7. On this page, you choose who will play the game. You can play another guest (or just keep the computer to yourself and play alone), you can let a friend or enemy log in, you can play an AI, or you can watch the two AI's play each other.
8. After submitting your choices, you roll the dice to decide who starts. Whoever get the highest dice roll gets the first turn. 
9. click start to begin your joyful Backgammon experience!
10. When you are playing, you get a button that allows you to roll the dice. After the roll, you get a list of buttons that represent the moves you are allowed to make. Hover over them to see what the move is. After you have used all of your dice, or if there are no valid moves, the turn is passed to the opponent.
11. Bear off all you pieces before your opponent to win the game!
12. Important! Make sure that you run "docker compose down" after you are done playing to shut down the database. The pgdata folder is a little unstable, so it is a good idea to shut it down just to be safe. Also, if you just run "docker compose up" again without shutting down and rebuilding, we find that the app doesn't always wait for the database before it tries to connect.

## In-depth project description
- On the home page we have the rules of Backgammon listed in case we have a user that is new to the game, or one who wants to fresh up on the rules before playing
- We give the option to register or log in. These forms should make sure that the user chooses a unique username, does not log in as the users that are supposed to be available (the two AIs and 'guest'), and checks for the correct password. If the user wants to play without having their stats stored - no worries! Just start a new game without logging in yet - we will get to this flow shortly
- The last button on the home page is the most important one - New Game. Click this button when you want to start playing! The most important functionality here before moving on to the actual game is about who actually gets to play. You get the option to play a guest player, play a friend, play the AI (with two different difficulties), or watch the AI play itself. If you want to play yourself, just choose 'guest' for one of the users, and yourself as the others! This is a great way to make your stats look better.
- If you want to play another user (non-guest), make sure they are already registered. This is to ensure that the newgame-experience is smooth to use. Also, when letting this player log in: we do not accept a sloppy login in the newgame-flow. If you fail to successfully log in, you are just assigned as a guest. Keep track of your usernames and passwords, it is an important lesson.
- About the AI: We have two AIs: easy (nicknamed 'steve') and hard (nicknamed 'joe'). We do not claim that any of them are difficult to play, we are only saying that one thinks slightly more than the other. Steve is an impatient soul, and always chooses the first move he sees. Joe, on the other hand, takes into consideration how many towers and blots he ends up with, and how many pips will be left for each player after the move - effectively taking into regard whether a piece is captured. We do not claim that this is an optimal or even a good strategy for playing the game, but it is a strategy.
- All common rules of backgammon should be implemented, with capturing and with bearing off only when pieces are in the home board, and the more complicated rules that follows bearing off. We list the possible moves for the user to choose from, so you can do each move with only a click of a button - this felt more convenient than the less efficient solutions out there.
- Note that if there are more than 6 pieces on a single triangles, they start to stack on top of each other, like it is done in traditional backgammon. So don't be scared if it looks like your pieces start to disappear - they are probably just stacking, they are still all there.
- We do not have a doubling die as we do not condone gambling. We also dont have a pause/resume button because we always encourage people to finish what they started - this is an important value of our team. 
- When a player is able to bear all their pieces off the board, the game is declared finished, and the players are taken to the "win" page, where the winner is clearly stated, and we present the options to play again or return to the home page
- We have a database running in the background. We have a user table that handles registering and logins, it stores all usernames and passwords. A second table stores user stats: number of games, wins, and losses for each of the users, including the AIs. The third table store information about each game: the last saved gamestate, the current status of the game (for instance 'finished'), the white and black player, and the winner (if there is one). Currently we only update this when the game is created and when it is finished, however this can be changed in the future.
- there is a scoreboard feature developed by a collaborating team, mainly done by Barry Nwike. Find this by navigating to the scoreboard endpoint by adding "scoreboard" to the URL. It was not completed by the time of writing, so I can't describe it further. If the group working on it were not able to merge it into main, it can be found in the DataVisual branch

## Project File Structure
Markdown:  
├── backgammon _(contains code associated with frontend, frontend API, and game logic)_  
&nbsp;|&emsp;├── app  
&nbsp;|&emsp;&nbsp;|&emsp;├── html _(directory containing html files/templates)_  
&nbsp;|&emsp;&nbsp;|&emsp;├── static _(directory containing css/images)_
&nbsp;|&emsp;&nbsp;|&emsp;├── api_functions.go _(contains helper functions for api.go)_  
&nbsp;|&emsp;&nbsp;|&emsp;└── api.go _(api to interface with a frontend)_  
&nbsp;|&emsp;├──  game  
&nbsp;|&emsp;&nbsp;&emsp;├── ai.go _(logic for AI players)_  
&nbsp;|&emsp;&nbsp;&emsp;└── gamelogic _(logic for rules and updating db)_ 
&nbsp;|&emsp;└── Dockerfile 
├── db  
&nbsp;|&emsp;├── db_setup.sql _(sets up db tables)_  
&nbsp;|&emsp;├── psqlConfig_master.py _(db credentials with read/write access)_  
&nbsp;|&emsp;└── psqlConfig_readaccess.py _(db credentials with read only access)_  
├── pgdata _(directory containing the postgresql db)_  
├── xx-Deliverable-1 _(Directory containing first deliverable for class about team contracts/project ideas)_  
├── pkg _(directory containing Go package objects)_    
├── compose.yaml _(Compose file to run all Dockerfiles. Sets up envionments/ports)_  
└── README.md   
  
    
Raw:   
├── backgammon (contains code associated with frontend, frontend API, and game logic)  
|   ├── app  
|   |   ├── html (directory containing html files/templates)  
|   |   ├── static (directory containing css/images) 
|   |   ├── api_functions.go (contains helper functions for api.go)  
|   |   └── api.go (api to interface with a frontend)  
|   ├── game   
|   |   ├── ai.go (logic for AI players)   
|   |   └── gamelogic (logic for rules and updating db)  
|   └── Dockerfile   
├── db  
|   ├── db_setup.sql (sets up db tables)   
|   ├── psqlConfig_master.py (db credentials with read/write access)  
|   └── psqlConfig_readaccess.py (db credentials with read only access)    
├── pgdata (directory containing the postgresql db)
├── xx-Deliverable-1 (Directory containing first deliverable for class about team contracts/project ideas)  
├── pkg (directory containing Go package objects)   
├── compose.yaml (Compose file to run all Dockerfiles. Sets up envionments/ports)     
└── README.md    
 

