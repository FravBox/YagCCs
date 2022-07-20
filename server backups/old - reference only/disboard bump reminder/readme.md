# These won't work anymore since Disboard uses slash commands now.

## Bump Commands

These are a set of CCs to use when you have disboard. You need all 3 CCs. It is all or nothing.    
First line of comments in each CC is for your reference. You do not have to include it in your actual CC.

Some of the text is specific to my server. It is also specific to disboard bump command but I figure it's probably easily editable to suit your needs. You could also have it mention a role instead of the user that clicked the reaction if you wanted, I guess.

## What it does    

### 2dbump.yag
you type `!d bump`, yag responds with a message with some reactions on it. This command cannot be triggered for another 2 hours in case anyone else uses the same command in that time.

### 1dbump-reaction.yag
Case 1: some user reacts with the specific emoji. This first user (only works for the first user) will be tagged in 2hrs to bump the server by executing another CC.    
Case 2: 1 minute passes without any reaction emoji clicked. The previous bump message is edited automatically encouraging other users to use the `remind` feature of yag. 

Line 28 which starts with `{{scheduleUniqueCC 15`.. You need to replace `15` with whatever the CC ID is of your `3reminderShout` command.

### 3reminderShout.yag 
I hit the max character limit in `1dbump-reaction`, so it got its own command here. This is the actual post yag sends 2hrs from the moment the user clicked the emoji on the previous CC's message.   
You need to find this CC's ID number in the Yag dashboard and replace `15` with this CC's ID number in `1dbump-reaction`.


