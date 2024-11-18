# THREAD MANAGEMENT - ABOUT 
**A set of custom commands for all sorts of thread features!**    

*The example images below may look slightly different from what you will experience. I've redone this CC quite a few times and reused the screenshots because I'm lazy.*

--------

# Main Features

**Auto-pins the first post in a thread +**
Sends a message about how to use the thread management tools     
(which detail all the things Thread OPs can do) 

[image here]

## Logging

See when threads are created and renamed.

![image](https://user-images.githubusercontent.com/20410737/181127576-629fedd2-bbbd-4cea-9557-281c96e0f3c0.png)      


## Announces thread creation

Tell people the thread was created in a news channel to boost engagement. (I throw it in one of the general chat channels.)

![image](https://github.com/FravBox/YagCCs/assets/20410737/d0b6f820-5e50-4ee4-95ae-5bc4ae5fa348)

## Manage Pinners (people who can pin messages)

Thread OPs and people with a mod role can add additional people as "pinners" who can manage pinned messages on their behalf.     
To toggle a person's pinner status, reply to any of their messages with `pinner`.     
You can also use reactions to do this.      
Anyone can use the text command `-pinners` to list who the pinners for that thread are.

![image](https://github.com/FravBox/YagCCs/assets/20410737/0ad77478-6697-43b6-ab76-f7c4704e8b26)

## Manage Pinned Messages

The Thread OP, a mod role, and any Pinners can pin and unpin messages in their thread.      
These people can use reactions or reply to any post with "pin" or "unpin" to pin/unpin the message they replied to.

![image](https://user-images.githubusercontent.com/20410737/181127916-5cd2e538-8a4b-467e-8c85-c9368a2e7b62.png)      

## Make a sticky message

Thread OPs & the mod role can use reactions or reply to any post with "stick" or "unstick" to make a message stick to the bottom of the thread.     
(This was added since thread pins are nearly impossible to find on mobile)

[image]


## Text commands for Mods

`-tcheck`     
Display database info

`-tsave`     
Resave db info - this will reset everything. Also has a emoji reaction counterpart.

`-tdel`     
Delete the db info (in most cases you'd want to use `-tsave` instead). Also has a emoji reaction counterpart.


# HOW TO INSTALL

3 commands are mandatory to install. The `mass delete db entries` is optional, but recommended.

**If you used an older version of this command**, you should delete and re-add all the thread management commands. Your databases will still work. Note that the `@everyone` and `@here` feature was removed.

## Add the commands

On your control panel, create a new command group for "Thread Management."     
As you add each command, name them similar to their filenames and keep note of their CC IDs.      
![14](https://github.com/user-attachments/assets/2fa88c13-2f1e-42de-974d-d49f7556824c) 

**1. Add `thread text commands.yag`**      
Its trigger type is none is you do not need to edit anything inside the command.

**2. Add `emoji thread management.yag`**     
Trigger type: reaction     
Trigger: added + removed reactions      
For `$base`, change the number to the number *after* the current CC ID. (e.g. if this CC ID is 6, put 7 here)

**3. Add `base thread management.yag`**     
Trigger type: Regex     
Trigger: `\A`

## Change the variables in `base thread management.yag`

### **Channels**

**`$news`**     
The Channel ID where new thread announcements go to boost engagement.     
If you don't want thread announcements, leave it at 0.

**`$log`**     
The Channel ID where new threads and thread renames go.     
If you don't want logs, leave it at 0.

### **Categories to ignore**

**`$ignore`**      
CATEGORY IDs (NOT channels).     
When we make public posts to `$news`, any threads in any of the channels in the `$ignore` categories will not be posted.      
You will want to put your moderation or other private CATEGORIES here.      
(You can find the category ID by right clicking on the category's name and then "copy channel ID". But make sure you're on the CATEGORY and not a singular channel.)      
Ignored categories can still use all commands. If you want to *completely* disable the thread system for certain channels or categories, use the channel restrictions on the control panel for the command group.

**`$logit`**    
Ignored categories do not get announced, but they do get logged. If you do NOT want logs for your ignored categories, change this to `1`.

### **Mod role**

**`$mod`**     
A role ID for who can use the moderation commands for the database. They can also do everything thread OPs can do.

### **Emojis**

**`$pin`**     
React with this emoji on a message to pin it and unreact to unpin.

**`$stick`**    
React with this emoji to sticky a message. Unreact to unsticky it.

**`$delpinner`**     
React with this emoji to remove the message's author from the pinner list.      
You can use the included file `delpinner.png` as the emoji or use your own.     
You will need to find the emoji ID to change this, as the current variable will NOT work as-is.     
You can find what you need to put here by typing the emoji into discord, putting a `\` directly in front of it, and then hitting enter.

**`$addpinner`**    
The same as the above, but for adding the message's author as a pinner.     
This will allow them to pin messages in addition to the Thread OP.

**`$success`**    
The emoji yag will use to tell you it successfully completed a command.    

**`$confuse`**    
The emoji yag will use to tell you that it knows you tried to use a command, but it either errored or can't figure out what you actually wanted to do.     
(e.g. you tried to remove a pinner but that person wasn't a pinner to begin with)

**`$save`**     
Mods can react with this emoji to re-save the thread information in the database. It will also reset the pinners & sticky.

**`$del`**     
Mods can react with this emoji to delete the database information.

### **Embed Colors**

These colors are used for the logs & announcement messages.    
They should be in decimal. You can find the decimal values for colors by using https://spycolor.com

**`$c1`**     
For new threads & thread announcements.

**`$c2`**    
For thread renames.

**`$c3`**    
For everything else.

### CC IDs
If you didn't change the CC ID in `emoji thread mgmt.yag` yet, do it now.

**`$txt`**    
CC ID of `thread text commands.yag`

**`$emoji`**     
CC ID of `emoji thread mgmt.yag`

### Seconds before the sticky is reposted

**`$len`**     
The command counts the seconds after a sticky message is posted. When a new person posts, it will check if the amount of time that has passed is the same or longer than this value.     
If you want the sticky post at the bottom *no matter what*, change this to `0`.     
However, 5 (the default value) is recommended in most cases.

## Optional Command

`mass delete db entries (optional).yag` deletes the top 100 db entries of threads that have been archived or deleted. 

The recommended use is to set it on an interval and allow it delete db entries of threads that are no longer active. You can do that with this setup:

Trigger: Hourly interval     
Interval: 168    
Channel: (choose any channel. It doesn't matter which one)

168 hours is one week. 

# Final Note
If you have trouble with this CC, feel free to try to contact me (@standardquip) in the YAGPDB support server.

However, I would highly recommend you instead try to figure out how this CC works and modify it to your own custom needs. It is very difficult to have a "universal" CC that covers something complex like this. It's much easier to hardcode in your own channel and category IDs and such (in my opinion).

If you happen to improve on this universal version of thread management CCs, please do a pull request or let me know your repo so I can link to you if people want alternatives. Thanks!