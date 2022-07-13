# Verification System

A simple verification system where users react with an emoji to a specific post to recieve a verification role. When the role is recieved, Yag announces the member as having joined the server in the main talk channel.

This command also logs when users have verified into a modlog, and, optionally, will also log incorrect verifications (if a user reacts to the wrong post) and/or delete emoji reactions.    
It supports having different channels for every step of the process.

**You only need the `verification.tmpl` for this code to work. `join.tmpl` and `leave.tmpl` are optional join & leave messages.**

Rules post that explains how to verify (not included in CC):    
![image](https://user-images.githubusercontent.com/20410737/177289398-53993d2f-db65-4e07-8929-7f4485879573.png)

Modlog version of join message (join.tmpl - optional) & verification (included in CC):    
![image](https://user-images.githubusercontent.com/20410737/177290969-8f0cf277-b792-45b5-b89b-4e7d16035ead.png)

When user verifies, this customizable message is posted to the main talk channel/non-modlog channel you specify:    
![image](https://user-images.githubusercontent.com/20410737/177293094-a892a982-dbe9-4bae-8632-6c6a7aa1c7b9.png)

(optional) modlog message of an incorrect verification post:     
![image](https://user-images.githubusercontent.com/20410737/177290088-41a74e34-083e-44ff-9b8c-249c238eba81.png)

(optional) Modlog post of a leave message (leave.tmpl):    
![image](https://user-images.githubusercontent.com/20410737/177291136-9e6c0cec-ac34-4d80-8a87-442e04d54e2c.png)

If you are already verified when you react to the correct post, you will be DMed that you're already verified and you won't be announced. Otherwise, users are not DMed at all.     
![image](https://user-images.githubusercontent.com/20410737/178642864-24bb1a30-0f37-4872-a0bd-e0d4aa4862c0.png)


# How to Use
Copy the `verification.tmpl` code into a custom CC.     
Make the trigger Reaction - added only.    
Set it to only run in the channel that contains the post users need to react to for verification.

Now, set all the variables (verification roleID, channel IDs, message IDs, etc.). The code is heavily commented.

Save, and you're done. System should just work.

# Suggested Server Setup
**Don't have an "unverified" role. Set your server permissions appropriately.**

**1. Set "everyone" SERVER permissions.**     
Set it so "everyone" does NOT have the ability to post or read anything. Set it as if it were your unverified role.

**2. Set "Verified" role SERVER permissions.**    
Explicitly give these users the ability to read and post to things. 

**3. Set Rules CHANNEL permissions.**    
For any channel you want EVERYONE to see, go into the CHANNEL permissions and make it so `@everyone` can read and (optionally) post to this specific channel.     
For the verification system cc to work here, they will also need the ability to react to messages.

Optionally, if you want a channel that ONLY unverified people can see, set the CHANNEL permissions so `@everyone` can read/write and `verified` can NOT view channel or read messages.     
In my server, I have 2 channels - Rules, which everyone can see, and lobby, which ONLY unverified people and mods can see. Lobby is just in case something goes wrong with the cc, yag is down, or whatever. It gives unverified people a way to talk to mods.

**4. Set the rest of the server's CHANNEL Permissions**    
For all "normal" channels, where you want verified to be able to act normally but you don't want unverified people to see/post anything, make sure default permissions for `@everyone` in channels is set to `/` and NOT X or the green checkmark.      
This covers everything. No need to manually add `verified` permissions to every channel created.

# Suggested CC Use

- Send joins, verifies, unsuccessful verifies, and leaves all to the same channel - e.g. `#joins-leaves`
- Send verification announcement (X has joined the server!) to whatever your main talk channel is.
- Use all the default values for the optional configs
