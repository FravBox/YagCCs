# Custom Report System

The up to date report system can be found [here](https://yagpdb-cc.github.io/moderation/report-system/overview) on the official CC Repo.     
However, I really don't like how that new updated one works! Luckily I have an old version. So here I am archiving the unchanged old version that I used in the FursuitReview Discord server, as well as the "new" version, which is the same as the old version but with a few updates that I use in AMV Sashimi.

**What it does**     
A user reports someone via `-report @user the reason`    
It has to be at least 2 words and they can't report themselves.

This sends an embed to the log channel with emoji reactions for mod actions.

![image](https://user-images.githubusercontent.com/20410737/178613458-069dfd85-8ff9-4690-b1c5-8973116753f1.png)

-----

**Only use one version.** Installing multiple versions will screw up your server.

----

## Old version info ( "Custom Reports v4" )

### Original Credits
**Custom Reports Main CC v4**     
    Made By Devonte#0745 / Naru#6203    
    Contributors: DZ#6669, Piter#5960, WickedWizard#3588      
    © NaruDevnote 2020-2021 (GNU GPL v3)    
	https://github.com/NaruDevnote/yagpdb-ccs 
	
**Custom Reports Message Tracker CC**     
    Made By Devonte#0745 / Naru#6203    
    © NaruDevnote 2020-2021 (GNU GPL v3)    
    https://github.com/NaruDevnote/yagpdb-ccs    
	
**Custom Reports ReactionListener CC v4**     
    Made By Devonte#0745 / Naru#6203     
    Contributors: DZ#6669, Piter#5960, WickedWizard#3588      
    © NaruDevnote 2020-2021 (GNU GPL v3)     
    https://github.com/NaruDevnote/yagpdb-ccs
	
**Custom Reports Admins CC v3**      
    Made By Devonte#0745 / Naru#6203     
    © NaruDevnote 2020-2021 (GNU GPL v3)     
    https://github.com/NaruDevnote/yagpdb-ccs
	
	

## New version info
It's the same as the old version, with the following fixes:    
- The responses to the original `-report` commands remove the user's ping and name and delete themselves after 10 seconds.
- Subheaders under "info" in the report embed are bolded.
- A new section was added to the report embed named "Legend" which tells you what all the emoji do.
- The correct error is returned when a mod tries to use an action they don't have the right perms for. (The old version always said you were unable to warn the user.)
- The comments at the top of each tmpl file were edited to reflect the updates.

# How to use both versions

**First, [go here](https://yagpdb-cc.github.io/moderation/report-system/overview) and follow the instructions to disable Yag's inbuilt report command.** You also need to make the command override it mentions.


Next, make 4 new custom commands. You need them all for the report system to function correctly.     
If you want to be organized, I highly recommend adding a new custom command group named "Report System" or something similar.

The instructions are in the comments at the top of each file, but they're summarized below as well:

**report1.tmpl**      
*Custom Reports Main CC v4*     
Trigger = Command: `report`     
Usable everywhere by everyone. (In places you want the `-report` command to work anyway)     
Stuff to change: `$logChannel` where the report embeds go      
`$ping` Role ID to ping when a report embed is made. Leave as 0 for no pings.

**report2.tmpl**      
*Custom Reports Message Tracker CC*    
Trigger = regex: `.*`     
Only run it in the log channel where reports go.     
Stuff to change: `$staff` cslice of RoleIDs for admins.

**report3.tmpl**      
*Custom Reports ReactionListener CC v4*     
Trigger = added reactions only      
Only run it in the log channel      
Stuff to change: `$logChannel` and `$staff` - this time `$staff` is all moderators.

**report4.tmpl**      
*Custom Reports Admins CC v3*     
Trigger = Regex: `\A-r(?:eport)?a(?:dmin)?(?:\s+|\z)`      
Restrict to roles that you want to be able to edit the report embeds.

This file includes the Report Admin Commands:     
(Command Aliases: ra, radmin, reporta)

`-ra reopen <messageID> <reason>` - Reopens a closed report.

`-ra resetreactions <messageID>` - Resets the reactions on a report
Aliases: rr

`-ra history <@User/ID>` - Displays the report history of a user

`-ra deletehistory <@User/ID>` - Deletes the report history of a user
Aliases: delhistory

`-ra reacthelp` - Reactions Help page.
