**Bump Commands**

These are a set of CCs to use when you have disboard. You need all 3 CCs. It is all or nothing.    
First line of comments in each CC is for your reference. You do not have to include it in your actual CC.

**What it does**    
2dbump.tmpl - you type !d bump, yag responds with a message with some reactions on it. This command cannot be triggered for another 2 hours in case anyone else uses the same command in that time.

1dbump-reaction.tmpl - Case 1: some user reacts with the specific emoji. This first user (only works for the first user) will be tagged in 2hrs to bump the server by executing another CC.  Case 2: 1 minute passes without any reaction emoji clicked. The previous bump message is edited automatically encouraging other users to use the ``remind`` feature of yag.

3reminderShout.tmpl - Because we couldn't fit the actual reminder/shout for the user who reacted without hitting the max character limit, it got its own command here. This is the actuall post yag sends 2hrs from the moment the user clicked the emoji on the previous CC's message.

-------

Some of the text is specific to my server. It is also specific to disboard bump command but I figure it's probably easily editable to suit your needs. You could also have it mention a role instead of the user that clicked the reaction if you wanted, I guess.
