# VERY Basic werewolf game
I had a fever dream so I coded this in about 3 hours. It's a text-based game where people in a channel collectively try to solve a werewolf problem. **It is NOT a social deduction game! No one is secretly a werewolf!**

Installing it and playing requires no coding knowledge. It will work as-is. However, I'm sure with just basic knowledge of regex and CCs, you could probably make this game much better and personalized.

## How to play

The game is so simple, that in order to make it fun, you should NOT actually tell the players how it works. They should only know the following rules:

---
**To interact with the werewolf:**    
You have to use simple commands.    
"I/we/the chat" does thing to/at "werewolf"    
(Your sentence has to begin with a pronoun and end with werewolf)    

If there was no response, that was not one of the commands. 

**Your goal is to get rid of the werewolf**    
(It is NOT a social deduction game; the bot is the werewolf)

Every message you make has an impact, even just chatting without actually doing anything to the werewolf.

---

# How to install

1. Create (or designate) a channel or thread for the werewolf game.
1. Make a new custom command GROUP on the YAGPDB dashboard and set it so the commands ONLY works in that channel
1. Add the command `setup.yag` and save
1. Add the command `wwgame.yag` and save
1. Go into your channel and run `-wwcreate`
1. Start playing the game


## Mechanics   
The game is, like I said, extremely simple. It starts with 1 werewolf at 100 HP. All werewolves have a shared HP pool, so additional werewolves double the HP pool. When HP reaches 0, the players win and the game is over.     
There is no losing condition.     
Players have an infinite amount of time to play.

It works by rolling a d100 for probability and a d10 for damage. It triggers on every single message, so simply talking will affect the game.    
Actual commands will have YAGPDB respond with a succeed/fail message.

## Types of commands

- `$chars` refers to message length. It is 50 by default. If a message is longer than `$chars`, there's a 20% chance of damaging the werewolf. If a message is shorter than `$chars`, there's a 10% chance the werewolf gains HP. This way, if your players never figure out what the commands are, simply talking still impacts the game and there is still a possibility of winning.
- Saying you want to be a werewolf adds 1 werewolf (doubles the current HP)
- The only attack that damages werewolves is throwing things at them. The cc looks for synonyms of "throw". e.g. "I throw something at the werewolf"
- Trying other types of attacks have a 50% chance of adding 1 werewolf (with the flavor saying that you got injured and you turned into a werewolf)
- If your players don't want to resort to violence, they can "make a cure for the werewolf." This has a 50% chance of success. You have an inventory and the game will keep track of how many cures you have.
- Players can then "give the cure to the werewolf." (throwing the cure destroys it!) This has a 10% chance of success, and if the game has more than one werewolf, it halves the HP. Otherwise, it is an instant game win.
- Players can perform a perception check with a 90% success rate. This will tell them: when the game started, how many werewolves there are, what the HP pool is, and how many cures they have in their inventory.


