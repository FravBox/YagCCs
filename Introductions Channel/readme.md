# Introductions Channel
Every member can post once in this channel. New posts are deleted. When the user leaves, the intro is also deleted. Can work for advertisement channels too.

**Requires specifying a role to allow people to post in the channel.** I have a verified role I use.

It logs when:
- someone posts their first intro
- someone tries to post another intro
- someone without the required role attempts to post an intro

It keeps the message content of the intro in the database. But due to how it functions (deleting new posts instead of old ones), it schedules another cc to update the message content an hour after someone posts.

This can work as-is, but you should probably know how to code a bit yourself to modify this exactly how you want. 

# Note before you continue
If someone makes their first post in the intros channel, then deletes it, the intro # in the database will be off and yag will not let that person post again. You will have to manually delete the db entry for that user when this happens. Alternatively, I wrote some extra commands near the end of this page.

# Set up
**0.** Open up `main command - intros.yag` in a text editor.    
**1.** In Discord, make or find the intros channel, and copy the channel ID to `$ch`    
**2.** Make the first post in the intros channel, then grab a link to that post. Put it in `$link`     
**3.** Grab the channel IDs for the channels you want to log intros in and put them in `$jl` for first time intros and `$log` for 2nd time intros.         
**4.** In discord, make or find the role ID for the role you want to require to post in the intros channel. Put this ID in `$role`.     
**5.** Go to the YAGPDB dashboard and add the entire `intro update.yag` command. Don't change anything. The trigger for this command is "none."     
Save it, and note the CC ID Number.     
https://media.discordapp.net/attachments/707661790443733022/764877102901362738/Screenshot_20201011_184823.jpg

**6.** Go back to the main command and input the CC ID of the CC you just saved for `$update`.      
**7.** Now you can save the main command in the YAGPDB dashboard. Set the trigger to be Regex `\A` and limit it so it ONLY runs in the intros channel.  

**8. To delete intros when a user leaves,** add `del intro on leave.yag` command to your leave message. Change `$modl` to the channel ID of your modlog.

# Optional companion command

`intro check.yag` is for anyone to use. It will give you info on your intro post if you made one, including a link to the message so you can edit it. Change `$ic` to the intros channel ID.

# In the case of deleted posts

If someone deleted their first intro post and yag won't let them post again, you can manually delete their intro db entry with the following command:
```go
{{/* manually delete intro db entry */}}
{{$args := parseArgs 1 (print "Please use the following format: `" .Cmd " <user>`")
    (carg "user" "Mention or ID")
	}}

{{$a := ($args.Get 0).ID}}
{{$intro := dbGet $a "intro"}}

{{if not $intro}}
    {{sendMessage nil (cembed "description" (print "<@" $a "> doesn't have an intro yet.") )}}
{{else}}
    {{dbDel $a "intro"}}
    {{sendMessage nil (cembed "description" (print "Deleted <@" $a ">'s intro.") )}}
{{end}}
```

Alternatively, you can let people delete their own intro posts & db entries with the following (don't edit anything):

```go
{{/* Users delete their own intro db entry 
trigger command: -delintro
*/}}

{{$idb := (dbGet .User.ID "intro")}}
{{$ich := $idb.Value.ch}}

{{if $idb}}
    {{deleteMessage $ich ($idb.Value.msg) 1}} 
    {{dbDel .User.ID "intro"}}
    {{sendMessage nil (print "Your intro was deleted. Feel free to post in <#" $ich "> again!") }}
{{else}}
    {{sendMessage nil "You haven't made a post in there yet!"}}
{{end}}
```


