# THREAD MANAGEMENT - ABOUT 
**A set of custom commands for all sorts of Thread features!**

**Table of Contents**       
1. Main features/pictures      
2. [Main mandatory command information.](https://github.com/FravBox/YagCCs/tree/main/Thread%20Management#main-command)     
    - Explanation between 2 different versions of main cc
    - [When db entries should expire](https://github.com/FravBox/YagCCs/tree/main/Thread%20Management#time---when-thread-db-entries-should-expire)
    - [Included text commands](https://github.com/FravBox/YagCCs/tree/main/Thread%20Management#included-text-commands)
    - [If you've ever used a previous version of these commands](https://github.com/FravBox/YagCCs/tree/main/Thread%20Management#install-this-command-first-if-youve-ever-used-an-older-version)
3. [Thread List command](https://github.com/FravBox/YagCCs/tree/main/Thread%20Management#thread-list-1)
4. [Installing the the thread management commands](https://github.com/FravBox/YagCCs/tree/main/Thread%20Management#installing-thread-management-commands)

`/learn/` contains heavily commented proof of concept code for saving a thread to the db and making a thread list command.       
You can use this to help you make your own thread-based commands. There's also some random facts I learned about threads in there.

## Database Management
![image](https://user-images.githubusercontent.com/20410737/181128287-fc0aab36-1158-446d-9c33-f69be6f46944.png)     
New threads will automatically be added to the database, but there are also commands to manually re-save and delete entries.

## Logging
![image](https://user-images.githubusercontent.com/20410737/181127576-629fedd2-bbbd-4cea-9557-281c96e0f3c0.png)      
See when threads are created, renamed, and manually resave the info to change who the thread author is.      
The logging part of the CC is entirely optional - You can still use the other features without it.

## Thread Authors & Pinning Messages
![image](https://user-images.githubusercontent.com/20410737/181127916-5cd2e538-8a4b-467e-8c85-c9368a2e7b62.png)      
The first person to post in a thread (usually the creator of the thread) can pin and unpin messages in their thread.      
Included in the main command, thread authors can reply to any post with "pin" or "unpin" to pin the message they replied to.
Optionally, an additional command can perform these actions with reactions.

## Emoji add-on
This will add the ability to pin, unpin, and re-save thread db information with message reactions.

## Thread List     
An add-on to the main custom command that will list all threads in your server. (Mostly) written by Shadow22A.
![image](https://user-images.githubusercontent.com/20410737/181121356-8bdb0456-798a-47e8-be3b-acc26dc2635b.png)      

## Mass Delete Database Entries
Written entirely by Shadow22A, this will delete the top 100 db entries of threads that have been deleted or archived. You can use this with a manual text trigger or put it on an interval to help clean up useless db entries and/or the thread list if you use that command often.


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

## Included text commands

`-tcheck`      
Checks if the thread you're in is in the database, and if it is, gives you the info associated with the entry. Only the staff role can use this.

`-tdel`      
Deletes the database entry associated with the tread you're currently in. Only the staff role can use this.

`pin` / `unpin`      
Reply to any message in a thread with "pin" or "unpin" and, if you are the thread author, yag will perform the action on the message you responded to. It will delete the mess ~10 seconds later. Only the thread authors can use this.

`save`     
Reply to any message in a thread to force re-save the thread database information. The author of the message you replied to will become the new thread author. Can only be used by the staff role.

## Install this command first if you've ever used an older version
I restructured what gets saved to the database, so if you've ever used an older version of this set of commands, upgrading won't work properly. You will have to clear all the old db entries and re-create them all. Apologies.

<details>
<summary>Click to view command</summary>

```go
{{/* deletes old db entries from prior versions of the thread management commands. Trigger type: command
trigger: -tdelall

Only use this once, then delete it.
*/}}


{{$catch := (print "*We reached an error, but this probably just means you didn't have any of these types of entries to delete, so don't panic.*\nThis was the error:\n" .Error)}}

{{/* deletes entries from the original logging CCs by Dei & Vars */}}
{{sendMessage nil "**1/3 Deleting any old logging db entries...**"}}

{{try}}
{{dbDelMultiple "ThreadCreate" 100 0}}
{{catch}}
{{sendMessage nil $catch}}
{{end}}


{{/* deletes entries from the original ThreadPins CC by Vars */}}
{{sendMessage nil "**2/3 Now deleting any old Thread Author/Pin db entries...**"}}
{{try}}
  {{dbDelMultiple "ThreadAuthor" 100 0}}
{{catch}}
  {{sendMessage nil $catch}}
{{end}}

{{sendMessage nil "**3/3 Finished.** \nYou can delete this command and install the new thread management CC now."}}
```
</details>


# Thread List
This command is very slow. YAGPDB WILL LAG WHEN YOU USE IT.      
Depending on how many db entries you range through and the amount of threads in your server, **it could take 5+ seconds to execute.** 

- It can only be used in channels, not threads
- It will NOT auto-update
- USE IT SPARINGLY

It does thread mentions and text links to the threads, so it should still work even if the threads get archived, as long as the db entries associated with them were not deleted.       
Many thanks to Shadow22A, who wrote 90% of this command.

## `$amt` - The amount of db entries to range through
The max is 100, but unless you have 100+ channels and/or threads, do not set it this high. The larger the number, the more command will lag. Adjust it to your server's needs.

# Installing Thread Management Commands
**0.** If you have ever used any of my old thread management commands, [use this command](https://github.com/FravBox/YagCCs/tree/main/Thread%20Management#install-this-command-first-if-youve-ever-used-an-older-version) to clear the old entries first. 

**1.** Pick either the original cc or the stripped down version. Do not use both.     
`thread db management main cc.yag` is the original and `thread db mgmt - stripped down version.yag` is the one that makes less db calls.

**2.** For the main cc, the trigger type is `regex` with the trigger type being `\A`, meaning it will trigger on every message. From there, edit all the variables noted before the "DO NOT EDIT BELOW" line.       
**The main cc is the only cc you need for thread logging and text commands. All other CCs are optional.**

A note - If you _currently_ have several threads open, whoever is the first to post in those threads after adding this cc becomes the "thread author." It will also generate a log that a thread was created. If you do not want log spam, you may want to disable logs, post in all your threads, then enable logs afterward.

**3.** Add any of the addons:     
- emoji addon allows you to pin, unpin, and resave threads with message reactions.
- mass delete db entries allows you to... mass delete invalid thread db entries. Mainly for use to clean up things for the thread list command.\
- thread list command will list all of the threads in your server.


