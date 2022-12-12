# License
You can use my (Vars#3616 / Fravbox) code & edit it however you want **except the stuff in server backups & things by people other than me.**     
If another user is credited, you must keep the credit in the code. If the code is in my server backups folder, please ask before using it.

# How To Use
Everything here assumes you can at least read basic code. I tell you what to edit for your server, but some are easier to use than others.

`server backups` is my personal server backups and aren't useful to outsiders.


<details>
<summary>Basic Starboard</summary>
Simplified starboard/pinboard without all the unecessary fancy crap. Replies to the message that was just moved (without pinging the original user) and quotes the message in the pinboard channel.
</details>

<details>
<summary>Custom Report System</summary>

Updates a really old version of a report system previously found in the official Yag CC repo, because I didn't like how the [current version](https://yagpdb-cc.github.io/moderation/report-system/overview) works.

Includes my version (new) and the original (old) version.

</details>

<details>
<summary>Delete Yag posts</summary>

Delete posts from YAGPDB with an emoji. Has several custom options.
</details>

<details>
<summary>Events</summary>

- Some give and take role reskins

- Enter Menu     
    Posts something similar to a role menu that assigns a role on reaction and automatically removes the role in 7 days if the user never unreacts later.

- 2wk Remind [ no longer works with sesh]     
    Yag detects the event title and timestamp from a message, calculates what the date will be 14 days prior to that timestamp, and posts a `!remind` command for that week prior date. For use with Sesh.fyi. 

</details>

<details>
<summary>Introductions Channel</summary>

Allows users to post once in a channel and then never again. Deletes new posts and keeps the original one. Logs when people make the first post and logs again when they make another attempt. Deletes the original post when the user leaves the server. Also good for advertising channels.
</details>

<details>
<Summary>LeaveBan</summary>
 
If someone is muted or timed out and then leaves while they're still muted/timed out, they are banned.
</details>

<details>
<summary>Misc</summary>

- Basic server stats     
- Improved bookmark commands      
- MessagePreview    
</details>

<details>
<summary>Prompts</summary>

A very basic system that allows users to submit prompts for writing, art, etc. Yag collects them, randomizes them, and then posts them periodically.

</details>

<details>
<summary>Reaction tickets</summary>

VERY Basic "make a ticket when clicking a reaction" command.

</details>

<details>
<summary>Templates</summary>

Random quick reference for snippets & templates.     
- random chance      
- cooldown      
- cooldown with branching      
- misc quick reference 
</details>

<details>
<summary>Thread Management</summary>
 
 * Thread Pins    
Allows the author of the first message in a thread to manage pins in the thread via post replies.

 * Thread Creation Log     
 Sends a log message to a specific channel when a thread is created

</details>

<details>
<summary>Verification System</summary>

An entire verification system based on reacting with a specific emoji to a specific post. Heavily commented, customizable, and has some picture examples.    
This is probably my most user-friendly code in the repo.

Also has a nice join and leave message template.

</details>

P.S. ~~I don't know how to code at all.~~ I now BARELY know how to code, but most of these are frankensteined together from various publicly available snippets/templates, context clues, and Yag support lmao. So while these all work, they might not be the most efficient.

# Misc Notes

Official [Yag Docs](https://docs.yagpdb.xyz/): [CC templates](https://docs.yagpdb.xyz/reference/templates), [functions](https://docs.yagpdb.xyz/reference/templates/functions), [custom embed info](https://docs.yagpdb.xyz/others/custom-embeds)    
[Yag CC github](https://github.com/yagpdb-cc/yagpdb-cc)

Other Yag CC Gits:    
[BlackWolf](https://github.com/BlackWolfWoof/yagpdb-cc) | [Crenshaw](https://github.com/Crenshaw1312/Yagpdb-ccs) | [Altair](https://github.com/magratheaguide/altair)

# Contact me
Open an issue or start a discussion on Github. I don't accept random friend requests, but my DMs are open. I'm in the official Yag support server if you want to DM or ping me from there. `Vars#3616`

**I won't code for you,** I don't know enough to do that. But I can explain my CCs or help you understand any errors you encounter with them.
