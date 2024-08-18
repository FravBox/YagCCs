# Voice Chat Management
Originally made to allow people to host their own events in stage channels without having permanent stage moderators, I extended basic functionality to all voice channels.    
**In theory this works, but it is untested.**   
I coded the entire thing and tested all the pieces. I have not tested the system as a single entity because I ended up going in a different direction and am not using this in my own server.    
**Test this before you use it in a public server.**

## Features
- An "interface" message with buttons which allow you to rent the "Stage host" role for a specific amount of time and un/mute people.
- Only people who are currently in a VC can become hosts
- Only one host at a time per VC
- There is a configurable maximum consecutive host time limit (default is 6 hrs)
- There is a configurable cooldown if you hit the max limit (default 1 hr)
- Only people who are currently in the same VC the host is in can be muted
- There is a configurable staff role that is immune from stage host mutes
- All the muted people are automatically unmuted when: 
 - The host manually unmutes them
 - The host's time/privileges expires
 - The host manually unhosts themself

## Downfalls
There are limits to Yag & Discord I had to work around... Here's the downfalls.
- Stage host mutes will only work if the yag mute has been configured (don't worry - stage host's mute role is not the same as yag mute role)
- In order to mute users, they must be disconnected from the VC first. So when a stage host mutes someone, the CC will also mute them through yag (and then immediately unmute them from yag, but keep them muted with the stage host's mute role)
- The above results in superfluous mod log entries & a mute DM.
- This CC assumes you will send the mute DM.
- Because you can only un/mute people who are in the same channel as you, you can't un/mute someone if they're not currently in VC at all. (You can edit the CC to allow this but I will not help you do that)
- If you do not set up your discord permissions correctly, a stage host's mute can mute someone from all VCs for the duration.

# How to Install

## \0. Set up your voice channels & roles
Make the following roles and *do not touch the permissions yet. Leave them at default.*    
If you will be using both stage channels and reular voice channels, make 2 different roles for stage hosts.    
Make a muted role.

Next, go to your channel list and create a category you want stage hosts to be able to operate in. Put the channels that will be hosted by stage hosts in this category.    
Depending on your needs, either adjust the permissions for the roles at the category or individual channel level. I'm going to assume you will be doing it by category for this setup.    
When all your channels have been created/moved to the category, go into the category permissions and add your roles.   
It is *here* where you will change your permissions for the roles.

If you have a stage channel: 1 role should be the minimum permissions required for stage moderators.    
If you use regular voice channels: No special permissions are required, but I would recommend granting at least  "Use Voice activity" and "set channel status."    
For the muted role: Explicitly disallow the following: Send voice messages, speak, video, use soundboard, use external sounds, use voice activity, set channel status, use activities, (optionally) request to speak

## \1. Go to the yag Dashboard > Moderation > Moderation > Mute    
If Yag's mute function is not already enabled and setup, enable it and set it up with a mute role. This is completely independent from the Stage host mute role. We just need *this* mute enabled so we can disconnect people from VCs temporarily, send notification DMs, and put things in the mod log (if you want that). Have the bot manage the role unless you know what you're doing.

This CC assumes you send mute DMs. The format that will make the most sense with this CC is the following:

**In the Mute DM:**    
```
You have been :mute: muted.
{{if .Reason}}{{.Reason}}{{end}}
```

**In the Unmute DM:**     
```
{{if eq .Reason "ignore"}}
{{return}}
{{end}}
You have been :loud_sound: Unmuted 
{{if .Reason}}{{.Reason}}{{end}}
```

## \2. Add the commands.
- Add `5min warning.yag` first. Take note of it's CC ID. It's trigger is `none`
- Add `vc mgmt components.yag` next. 
 - trigger type is `message component`
 - trigger regex is `^vc-`
 - add 5min warning's CC ID to line 8 `$ccid`
 - Put the role IDs for your stage host roles in lines 11 & 12. If you don't have a stage channel, use the same role ID for both.
 - add the role ID for the muted role (the one stage hosts will assign, not yag's) in line 15
 - change the limits if you want (I recommend keeping the defaults)

- Add `interface.yag`
 - The trigger can be whatever you want. I personally designed this to be posted in a locked channel once and then never used again, but you do you.

 ## \3. Use the command for the interface somewhere.
 I designed this to be used in a permanent channel that is locked from posting by all roles, but it will still work if you only want it as a text command. 

 In any case, use the command somewhere to post the interface. Make sure you're connected to a voice channel, and then use the interface to start hosting & muting people. Enjoy!

 ### Final Notes
 I will not be updating this cc unless it's a very easily fixed issue, but I will approve PRs. No new features will be added. 

 My code is heavily commented so you should be able to modify it if you have experience with custom commands. If you have questions you can ping me (`@standardquip`) in the yag support server to explain how/why I did something, but I will not update the code myself or code for you.
