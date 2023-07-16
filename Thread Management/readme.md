This will work as-is but it is currently missing the (updated) thread list part.
To do:
- thread list cc
- add images
- finish writing how to install and such

# THREAD MANAGEMENT - ABOUT 
**A set of custom commands for all sorts of Thread features!**    
There are 4 custom commands. You must use at least 2 of them. The other 2 are optional.

**Table of Contents**       
1. Main features/pictures      
2. 
3. 

--------


## Auto-pins first post in a thread
[SCREENCAP OF 1ST MESSAGE]
Also sends a message about how to use the thread management tools.

## List of Active Threads -  one post per category
[SCREENCAP OF THREAD LIST]
Makes one message per category, based on the category the command is run in.     
Edits previous message if it exists, otherwise makes a new post.

## Logging
![image](https://user-images.githubusercontent.com/20410737/181127576-629fedd2-bbbd-4cea-9557-281c96e0f3c0.png)      
See when threads are created and renamed.

## Manage Pinners (people who can pin messages)
[SCREENCAP OF PINNERS COMMANDS]
Thread OPs and people with a mod role can add additional people as "pinners" who can manage pinned messages on their behalf.     
To toggle a person's pinner status, reply to any of their messages with `pinner`.     
There's an emoji add-on that can use reactions to do this.      
Anyone can use the text command `-pinners` to list who the pinners for that thread are.


## Manage Pinned Messages
![image](https://user-images.githubusercontent.com/20410737/181127916-5cd2e538-8a4b-467e-8c85-c9368a2e7b62.png)      
The Thread OP, a mod role, and any Pinners can pin and unpin messages in their thread.      
Included in the main command, these people can reply to any post with "pin" or "unpin" to pin/unpin the message they replied to.
Optionally, an additional command can perform these actions with reactions.

## Mention `@Everyone` and `@Here`
[SCREENCAP OF EVERYONE AND HERE]
If Thread OPs mention `@everyone` or `@here`, Yag will make sure those people are pinged inside the thread.    
(note these only ping everyone who is currently a member of the thread, not all user of a server)

## Text commands for Mods
`-tcheck`     
Display database info

`-tsave`     
Resave db info - this will reset all the pinners

`-tdel`     
Delete the db info (in most cases you'd want to use `-tsave` instead)

`-tlist`     
Manually force an update for that category's thread list

`-tlistdel`    
Delete the records for the thread list messages and start over. This will not delete the thread list messages that were posted previously.

## Mass Delete Database Entries for Archived Threads
This will delete the top 100 db entries of threads that have been deleted or archived. You can use this with a manual text trigger or put it on an interval to help clean up useless db entries and/or the thread list if you use that command often.


# HOW TO INSTALL

## If you used an older version of this command
This is backwards compatible!    
<details><summary>But here are the functional changes you might care about</summary>
details here
</details>

## REQUIRED COMMANDS
You MUST install `tlist.yag` and EITHER `master base thread management.yag` OR `emoji thread mgmt.yag`.     
Without `tlist`, the commands will not work.

However, the commands were designed to use all four files. So I'd recommend installing them all.

## Install tlist.yag FIRST
Take note of the CCID. You will need it for later.
[stuff you edit in that command here]

## REQUIRED EDITING
**There are a lot of things to edit before the cc will work!!**      
See instructions below for each CC.

<details><summary>Master base thread management.yag</summary>
instructions
</details>

<details><summary>emoji thread mgmt.yag</summary>
instructions
</details>

<details><summary>delete old db entries automatically.yag</summary>
instructions
</details>
