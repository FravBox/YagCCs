# Ping Lists

## This might not actually work, sorry. 
You can create a personalized ping list for informal events! You must install both commands for it to work.

**Create a ping list**
`create pinglist` will post a message letting people react to add themselves to the pinglist. If you add mentions in this message, they will be auto-loaded into the pinglist on creation.
e.g. `create pinglist @Vars` will create a pinglist with Vars on it.
Keep in mind that you cannot add roles, `@everyone`, or `@here` to a ping list.

**Edit a ping list**
`edit pinglist` works similar to `create`. Without mentions, it will repost the message allowing people to add or remove themselves from the list.
If you have mentions in the message, it will add those people onto the list you had before - e.g. `edit pinglist @Yag` will add Yag to the list of people already mentioned.

**Ping the people on the ping list**
Type `@pinglist` to have Yag ping your list.

**Delete or create a new ping list**
You can only have one ping list at a time. The lists automatically expire after one month by default.
Using `create pinglist` will replace a current ping list with a new one.

**Please note:**
Any time you do any function with the ping list, it will delete the last ping list message and repost it. 
This is so you do not have multiple signup messages for your ping list.

![](https://bentovid.com/user/pages/03.sguides/04.bot-commands/pinglist.png)
