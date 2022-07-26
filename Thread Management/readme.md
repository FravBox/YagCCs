# CURRENTLY DOING A MASSIVE UPDATE
I can't update git in an optimal way so sorry if you have to see this (should be max an hour)




# THREAD MANAGEMENT
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



# Notes
**If you're using my code to help you make your own codes that involve threads, please read these notes**      
If the message in the main channel that says "X started a thread" ever gets deleted, the `.Message.Author` comparison won't work. This is why my CCs save the author to database.

Message type 21 is the thread creation message. But you can't use this in a CC to detect when a thread is created, because if anyone makes a thread via the plus icon in the message bar instead of using a pre-existing message to create a thread from, it will not fire. This is why my cc doesn't use message types.
