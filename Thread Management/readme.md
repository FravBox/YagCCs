# CURRENTLY DOING A MASSIVE UPDATE
I can't update git in an optimal way so sorry if you have to see this (should be max an hour)




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


# MAIN COMMAND
** There are two versions of the main command. ONLY USE ONE! Here's how to choose.**

Main cc has 1 db call for every message. There are 2 commands with 5 calls in one message.     
**This means the cc will stop working when:**      
for free servers:      
- 10+ threads get posted in at the same time, or      
-  2+ threads get renamed or resaved at the same time

for premium servers:      
- 50+ threads get posted in at the same time, or      
- 10+ threads get renamed or resaved at the same time

If you have a LOT of threads, or your threads are extremely active, please use my stripped down version of this cc, which logs slightly less info but makes far less db calls.

**CC Differences:**

Normal:       
- 1 db call for every message      
- Up to 5 db calls when information changes      
- Always updates the db, and all logs read from the db, so you can be sure what you are seeing is actually in the db.      
It also always keeps the previous thread name and the previous author when a thread is renamed, both of which show up in the logs.

Stripped down:     
- 1 db call for every message      
- Max 2 db calls when information changes (possibly 3 if you're logging everything)      
- Tries to avoid doing db calls if logging is disabled.      
- Logs don't read from the db, but rather get the information that *should've* been saved to the db.     
- tcheck command reads slightly delayed version of db. It might not be accurate if you just changed your thread 3+ times in a row.       
- **Whoever renames the thread becomes the new thread author.**        
(Thread creators can rename their own threads without mod priviledges in discord, so this will only be an issue if you have staff frequently renaming threads)

**The addons will work with both versions of the main cc.**

## `$time` - When threads db entries should expire
If someone posts in a thread past the database expiration, it will post a new log for the thread as if it were just created.        
You can make the db entry last for several years, but this is unecessary in most cases. Please adjust the time to your server's needs, so it expires some time after people normally stop using the threads.


# Thread List
This command is very slow. YAGPDB WILL LAG WHEN YOU USE IT.      
Depending on how many db entries you range through and the amount of threads in your server, it could take 5+ seconds to execute. 

- It can only be used in channels, not threads
- It will NOT auto-update
- USE IT SPARINGLY

It does thread mentions and text links to the threads, so it should still work even if the threads get archived, as long as the db entries associated with them were not deleted.




# Notes
**If you're using my code to help you make your own codes that involve threads, please read these notes**      
If the message in the main channel that says "X started a thread" ever gets deleted, the `.Message.Author` comparison won't work. This is why my CCs save the author to database.

Message type 21 is the thread creation message. But you can't use this in a CC to detect when a thread is created, because if anyone makes a thread via the plus icon in the message bar instead of using a pre-existing message to create a thread from, it will not fire. This is why my cc doesn't use message types.
