# Save threads to db and make a thread list

In the process of making this group of CCs, I learned a lot. Here is the "proof of concept" CC, with a quick way to save a thread to the database and a pre-made thread list. The code is heavily commented so you can modify it to your own wants and maybe make your own CC for thread management.

**This is not a CC you should use outside a testing atmosphere. It is made to learn from and modify, not to actually use.**

![image](https://user-images.githubusercontent.com/20410737/181144830-1e4ff7a1-f922-4d0d-99fa-f00a36efab9a.png)


# Things you should know about threads when making Custom Commands
If the message in the main channel that says "X started a thread" ever gets deleted, the `.Message.Author` comparison won't work. This is why my CCs save the author to database.

Message type 21 is the thread creation message. But you can't use this in a CC to detect when a thread is created, because if anyone makes a thread via the plus icon in the message bar instead of using a pre-existing message to create a thread from, it will not fire. This is why my cc doesn't use that message type.

When threads are archived, their channel mentions will appear as `#deleted-channel` and internally, Discord will treat these threads as if they no longer exist, despite the fact that they can be unarchived. This is part of the reason why every action that uses thread mentions also uses text links. The other reason is that thread mentions do not work reliably even when the thread isn't archived - The result varies across platforms.

Related, the thread list CC was unecessarily convulted because I specifically wanted to list archived threads, too. Using `with` or `.Channel.Mention` will automatically exclude all archived threads, because to Discord, those don't exist anymore. ¯\_(ツ)_/¯

The link structure for all threads is: `https://discord.com/channels/GuildID/ChannelID`

When threads are renamed, a message is always posted notifying of the rename. This is message type 4. The author of this message type is the person who renamed the thread (which can include a thread creator without mod permissions). The new name of the thread is the _only_ message content when using `reFind`.

### When `#deleted-channel` will appear for threads
- After some unknown cache time after a thread is archived (could be a day, could be a week)
- If you're viewing the thread mention from iOS and the thread mention is for a thread that's parent channel is not the channel you're currently in (even if the thread isn't archived)
- The above, but for archived threads you are not and/or never have been a member of
- If you are not a member of the thread mentioned and/or you never were a member, an archived thread will always be `#deleted-channel`

-----------

If you have any questions about threads or any interesting discoveries related to writing CCs concerning them, please feel free to contact me here or over Discord to tell me about them! Thanks.
