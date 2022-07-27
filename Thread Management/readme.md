# THREAD MANAGEMENT - ABOUT 
A set of custom commands for all sorts of Thread features!

Table of contents will go here as this will be a long readme

## Logging
![image](https://user-images.githubusercontent.com/20410737/181127576-629fedd2-bbbd-4cea-9557-281c96e0f3c0.png)      
See when threads are created, renamed, and manually resave the info to change who the thread author is.      
The logging part of the CC is entirely optional - You can still use the other features without it.

## Thread Authors & Pinning Messages
![image](https://user-images.githubusercontent.com/20410737/181127916-5cd2e538-8a4b-467e-8c85-c9368a2e7b62.png)      
The first person to post in a thread (usually the creator of the thread) can pin and unpin messages in their thread.      
Included in the main command, thread authors can reply to any post with "pin" or "unpin" to pin the message they replied to.
Optionally, an additional command can perform these actions with reactions.

## Thread List     
![image](https://user-images.githubusercontent.com/20410737/181121356-8bdb0456-798a-47e8-be3b-acc26dc2635b.png)      
An add-on to the main custom command that will list all threads in your server.

## Database Management
![image](https://user-images.githubusercontent.com/20410737/181128287-fc0aab36-1158-446d-9c33-f69be6f46944.png)     
New threads will automatically be added to the database, but there are also commands to manually re-save and delete entries.

## Emoji add-on
This CC is optional and will add the ability to pin, unpin, and re-save thread db information with message reactions.


# MAIN COMMAND
**There are two versions of the main command. ONLY USE ONE! Here's how to choose.**

Main cc has 1 db call for every message. There are 2 commands with 5 calls in one message. This is important, as YAGPDB has database interaction limits.

**This means the cc will stop working when:**      
for free servers:      
- 10+ threads get posted in at the same time, or      
-  2+ threads get renamed or resaved at the same time

for premium servers:      
- 50+ threads get posted in at the same time, or      
- 10+ threads get renamed or resaved at the same time

If you have a LOT of threads, or your threads are extremely active, please use my stripped down version of this cc, which logs slightly less info but makes far less db calls.

__**CC Differences:**__

**Normal:**       
- 1 db call for every message      
- Up to 5 db calls when information changes      
- Always updates the db, and all logs read from the db, so you can be sure what you are seeing is actually in the db.      
It also always keeps the previous thread name and the previous author when a thread is renamed, both of which show up in the logs.

**Stripped down:**     
- 1 db call for every message      
- Max 2 db calls when information changes (possibly 3 if you're logging everything)      
- Tries to avoid doing db calls if logging is disabled.      
- Logs don't read from the db, but rather get the information that *should've* been saved to the db.     
- tcheck command reads slightly delayed version of db. It might not be accurate if you just changed your thread 3+ times in a row.       
- **Whoever renames the thread becomes the new thread author.**        
(Thread creators can rename their own threads without mod priviledges in discord, so this will only be an issue if you have staff frequently renaming threads)

**The addons will work with both versions of the main cc.**

## `$time` - When thread db entries should expire
If someone posts in a thread past the database expiration, it will post a new log for the thread as if it were just created.        
You can make the db entry last for several years, but this is unecessary in most cases. Please adjust the time to your server's needs, so it expires some time after people normally stop using the threads.

## Included text commands.

`-tcheck`      
Checks if the thread you're in is in the database, and if it is, gives you the info associated with the entry. Only the staff role can use this.

`-tdel`      
Deletes the database entry associated with the tread you're currently in. Only the staff role can use this.

`pin` / `unpin`      
Reply to any message in a thread with "pin" or "unpin" and, if you are the thread author, yag will perform the action on the message you responded to. It will delete the mess ~10 seconds later. Only the thread authors can use this.

`save`     
Reply to any message in a thread to force re-save the thread database information. The author of the message you replied to will become the new thread author. Can only be used by the staff role.

# Install this command first if you've ever used an older version
I restructured what gets saved to the database, so if you've ever used an older version of this set of commands, upgrading won't work properly. You will have to clear all the old db entries and re-create them all. Apologies.

[Command TBA soonish]



# Thread List
This command is very slow. YAGPDB WILL LAG WHEN YOU USE IT.      
Depending on how many db entries you range through and the amount of threads in your server, **it could take 5+ seconds to execute.** 

- It can only be used in channels, not threads
- It will NOT auto-update
- USE IT SPARINGLY

It does thread mentions and text links to the threads, so it should still work even if the threads get archived, as long as the db entries associated with them were not deleted.

## `$amt` - The amount of db entries to range through
The max is 100, but unless you have 100+ channels and/or threads, do not set it this high. The larger the number, the more command will lag. Adjust it to your server's needs.

# Installing Thread Management Commands
0. If you have ever used any of my old thread management commands, use this command to clear the old entries first. (TBA)

1. Pick either the original cc or the stripped down version. Do not use both.     
`thread db management main cc.yag` is the original and `thread db mgmt - stripped down version.yag` is the one that makes less db calls.

2. For the main cc, the trigger type is `regex` with the trigger type being `\A`, meaning it will trigger on every message. From there, edit all the variables noted before the "DO NOT EDIT BELOW" line.       
**The main cc is the only cc you need for thread logging and text commands. All other CCs are optional.**

3. Add any of the addons:     
- emoji addon allows you to pin, unpin, and resave threads with message reactions.
- mass delete db entries allows you to... mass delete invalid thread db entries. Mainly for use to clean up things for the thread list command.\
- thread list command will list all of the threads in your server.




# Notes
**If you're using my code to help you make your own codes that involve threads, please read these notes**      
If the message in the main channel that says "X started a thread" ever gets deleted, the `.Message.Author` comparison won't work. This is why my CCs save the author to database.

Message type 21 is the thread creation message. But you can't use this in a CC to detect when a thread is created, because if anyone makes a thread via the plus icon in the message bar instead of using a pre-existing message to create a thread from, it will not fire. This is why my cc doesn't use message types.
