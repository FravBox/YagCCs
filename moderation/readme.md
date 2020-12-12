The files are the CCs I use to send the help DMs. Below is what is listed in the help DMs.

# Mod Bot Commands 
 @Lead and @Staff can use ALL commands listed here.     
 Be warned! <ins>Using the bot will DM the user every time.</ins>      
If you instead use Discord's native kick or ban functions, you can yeet people without them knowing what happened.      
You can use these commands in any channel. What you type is immediately deleted by the bot while it takes action. 

All actions using the bot are automatically logged in #warnings-bans. If you don't use the bot, remember to manually type your action in that channel.      
Also relevant: Last 100 messages and any messages that were deleted within the last hour are logged when any mod action through the bot is taken. These logs are only viewable to people with YAGPDB Control Panel access. 
 
 **Muting**      
`-mute @user <duration in minutes (optional)> <reason (mandatory)>`     
Example:     
`-mute @Vars 30 Stop being a dip`     
Mutes Vars for 30 minutes.     
`-mute @Vars Don't spam`     
If no duration is specified, it will be 10 minutes.

YAGPDB gives people the role Muted which prevents them from sending or reacting to messages in the server, but they can still see everything. 
A mute DM tells the user who muted them and the reason.     
`-unmute @User <reason (optional)>`     
This will remove the Muted role allowing the user to participate again. You don't have to use this as it will happen automatically at the specified time.      
Note: If you specify 0 as the duration, the mute is permanent.

**Warnings**     
 `-warn @user <reason (mandatory)> `    
The DM sent will tell the user who warned them. 
 
`-warns @User`     
Will PUBLICLY DISPLAY a list of all warnings for a user. Careful using it.     
You can use the actual ID of a user if you have dev mode enabled. This will prevent a mention (this ID is not the same as the number in a username).

`-topwarns`       
PUBLICLY shows ranked list of warnings on the server.      
Only use this in #modtalk     
 
**Kicking**     
`-kick @user <reason (mandatory)>`      
Kicking through discord doesn't require a reason, but doing it through the bot does. DMs to the user don't say who kicked them. 
 
**Permanent Bans**     
`-ban @user <reason (mandatory)>`    
Reasons are mandatory for the bot, but not when using discord's native ban.     
Using the bot won't delete any banned user messages, but using discord's ban function allows for the option.     
DMs sent to user don't mention who banned them.    
Everyone can use the bot ban, but @Staff can't use discord's native ban.
 
You can call this DM by using `-modhelp` in any server, but the mod will reply saying it sent a DM. So you may only want to use this command in #modtalk to avoid suspicion.
