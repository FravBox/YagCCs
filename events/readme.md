# Event Stuff
`elead`
`enter`
`staff`
These all just reskin Yag's grole command to use a different trigger. Probably not useful.

`exit`
`noelead`
`nostaff`
These take away the roles given with the previous commands. Probably not useful.

### Enter Menu
3 files, 3 CCs, you need all 3 for this to work. **Make sure to limit this to a particular set of channels/roles; it's very easy to abuse**.     
In my server, verified users are allowed to create their own channels for events. If they want to easily ping people participating in their events, they ping a specific role. We created this menu for people to easily self-assign the role during events in order to create that ping list. 

The user submits `-entermenu`    
This creates a message with a 🏆 reaction on the message. Anyone who uses that reaction is given a role ("entrant" - You need to change the name/role ID for your server).    
This role is automatically removed in 7 days, or if the user unreacts to the message. 

It also creates a second message right after the first. This 2nd message just says "It's recommended you pin the above message to the top of your channel."   
This second message deletes itself after 30 seconds.

`entermenu1`   
You don't have to change anything

`entermenu2`   
Change `RoleIDToUse` to... the Role you want to use. (Could also work with a cslice I suppose)     
`TimeInSeconds` is how long to wait before removing the role if the user never un-reacts. By default it's 7 days.    
The Author ID refers to Yag specifically - don't change/delete this or it will run the enter menu any time anyone replies with a trophy emoji.   

`entermenu3`   
The `RoleIDToRemove` should be the same roleID(s) used in `entermenu2`.   
Again, Author ID refers to Yag specifically.

### 1wk Remind

Yag detects the event title and timestamp from a message, calculates what the date will be 7 days prior to that timestamp, and posts a `!remind` command for that week prior date. For use with Sesh.fyi. Further explanation in the file.
