# Tag system extras
These are optional text commands for edge-case needs

## Change tag author
`-tagauthor TagRefMessageURL @NewAuthor`     
Change a tag's author to someone else. Useful after migration. You can use a User ID instead of a ping if you want.      
Note this does not update the original tag reference message (it will still show the old author). If you want to update the ref post, manage the tag by saving it without actually changing anything.

## Check tag info
`-taginfo TagMessageURL`     
Shows all the metadata/db info for a specific tag.     
Displays raw markdown for current & previous tag content.

## Manage master alias list
`-aliaslist`     
Prints out the master alias list and the command needed if you want to overwrite it for some reason.      
Do NOT use this if you could not have written this command yourself.

## Repost missing tag refs
`-tagrepost`     
The main admin command has a button to delete tags without reference posts. This command does the opposite, and will repost tags that currently don't have reference posts.      
It will most likely spit out an error message, so use it some place private.