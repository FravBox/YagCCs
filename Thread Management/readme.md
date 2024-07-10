# THREAD MANAGEMENT - ABOUT 
**A set of custom commands for all sorts of Thread features!**    
There are 2 custom commands. You should use both, but it will work with only 1 (`master base thread management.yag`). If you plan to only use 1, you will probably have to edit the code more than what the initial install requires.

The example images below may look slightly different from what you will experience. I've redone this CC quite a few times and reused the screenshots because I'm lazy.

--------

# Main Features

## Auto-pins first post in a thread

Also sends a message about how to use the thread management tools.

![image](https://github.com/FravBox/YagCCs/assets/20410737/7e060596-8197-4808-81d2-6ea2961ca863)


## Logging

![image](https://user-images.githubusercontent.com/20410737/181127576-629fedd2-bbbd-4cea-9557-281c96e0f3c0.png)      
See when threads are created and renamed.

## Announces thread creation

![image](https://github.com/FravBox/YagCCs/assets/20410737/d0b6f820-5e50-4ee4-95ae-5bc4ae5fa348)


Tell people the thread was created in a news channel to boost engagement. (I throw it in one of the general chat channels.)

## Manage Pinners (people who can pin messages)

![image](https://github.com/FravBox/YagCCs/assets/20410737/0ad77478-6697-43b6-ab76-f7c4704e8b26)


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

If Thread OPs mention `@everyone` or `@here`, Yag will make sure those people are pinged inside the thread.    
(note these only ping current members of the thread, not all user of a server)

## Text commands for Mods

`-tcheck`     
Display database info

`-tsave`     
Resave db info - this will reset all the pinners. Also has a emoji reaction counterpart.

`-tdel`     
Delete the db info (in most cases you'd want to use `-tsave` instead). Also has a emoji reaction counterpart.


# HOW TO INSTALL

There are 2 commands. You should use both. Add `master base thread management.yag` first. This handles the thread database and all the text commands.      
The second command is `emoji thread mgmt.yag` which lets you use emoji reactions so you don't have to type commands.

**If you used an older version of this command**      
This is backwards compatible!    
<details><summary>But here are the changes you might care about</summary>
- This works for all free users; you shouldn't have to worry about hitting db limits anymore.
- Old CC guessed who the thread OP was. This version *actually knows* who the Thread OP is.
- I took out the "thread list" part completely. There's just no way to make this universally work for everyone. Please code your own custom solution; sorry.
- Otherwise, this is functionally the same CC but with the added "pinners" and "@everyone/here" features.
</details>


## **There are a lot of things to edit before the cc will work!!**      

## master base thread management.yag

**Variables to change**

**`$news`** is a public channel where you want to annouce that a new thread has been created. Put its channel ID here.

**`$log`** is the channel ID of where you want the posts about threads being created, renamed, etc.

**`$ignore`** are CATEGORY IDs (NOT channels). When we make public posts to `$news`, any threads in any of the channels in the `$ignored` categories will not be posted. You will want to put your moderation or other private CATEGORIES here. (You can find the category ID by right clicking on the category's name and then "copy channel ID". But make sure you're on the CATEGORY and not a singular channel.)

**`$staff`** is the Role ID for who can use the moderation commands for the database. They will also always be able un/pin messages.

**emojis** this section is for telling the command what emojis to look for for certain functions.    
`$pin` React with this emoji on a message to pin it and unreact to unpin.    
`$delpinner` React with this emoji to remove the message's author from the pinner list. You can use the included file `delpinner.png` as the emoji or use your own. You will need to find the emoji ID to change this, as the current variable will not work as-is. You can find what you need to put here by typing the emoji into discord, putting a `\` directly in front of it, and then hitting enter.

`$addpinner` is the same as the above, but for adding the message's author as a pinner. Which will allow them to pin message sin addition to the Thread OP.

`$success` is the emoji yag will use to tell you it successfully completed a command.    
`$confuse` is the emoji yag will use to tell you that it knows you tried to use a command, but it either errored or can't figure out what you actually wanted to do. (e.g. you tried to remove a pinner but that person wasn't a pinner to begin with)

**embed colors** is the section for the logs. Change the color based on the type of log message. Use decimal for colors. You can find the decimal colros at https://spycolor.com

Don't edit anything else if you don't know how to code.

## emoji thread mgmt.yag

This command has the emojis section, the mod role (`$staff`), and the embed colors section to change. Make sure the values are the same as the ones you used in the first command.  

It has 2 additional emojis, however:

**`$save`** is an emoji that will allow mods to re-save the thread information in the database by reacting to any message in the thread. It will also reset the pinners.

**`$del`** is the emoji for mods to delete the database information.

Don't edit anything below the `do not edit below` line.

# Final Note

If you have trouble with this CC, feel free to try to contact me (@standardquip) in the YAGPDB support server.      
However, I would highly recommend you instead try to figure out how this CC works and modify it to your own custom needs, instead. It is very difficult to have a "universal" CC that covers something complex like this. It's much easier to hardcode in your own channel and category IDs and such (in my opinion). 

If you know how to code, you can look at what I currently use for the thread management in my server, [here](https://github.com/FravBox/YagCCs/tree/main/z_server%20backups/thread%20control/2023%20thread%20mgmt). (Note that copy/pasting that into your CCs WILL NOT WORK.). I comment my code pretty heavily, so hopefully it's easy enough to read.

If you happen to improve on this universal version of thread management CCs, please do a pull request, or let me know your repo so I can link to you if people want alternatives. Thanks!
