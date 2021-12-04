# Event Stuff
`elead`
`enter`
`staff`
These all just reskin Yag's grole command to use a different trigger. Probably not useful.

`exit`
`noelead`
`nostaff`
These take away the roles given with the previous commands. Probably not useful.

# Enter Menu
3 files, 3 CCs.

This creates a message with a 🏆 reaction on the message. Anyone who uses that reaction is given a role ("entrant" - You need to change the name/role ID for your server). 
This role is automatically removed in 7 days, or if the user unreacts to the message. 

It also creates a second message right after the first. This 2nd message just says "It's recommended you pin the above message to the top of your channel."
This second message deletes itself after 30 seconds.

`entermenu1`
You don't have to change anything

`entermenu2`
The Author ID refers to Yag specifically - don't change/delete this or it will run the enter menu any time anyone replies with a trophy emoji.
RoleID needs to be changed to the role you want to assign/remove.
`604800` is not a roleID - it is the time. In this case it's 7 days.

`entermenu3`
only edit the removeRoleID.
Again, Author ID refers to Yag specifically.
