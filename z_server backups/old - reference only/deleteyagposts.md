Use trashcan emoji to delete any yag post. Doesn't quote the VPR messages to save space.       
Modified from the main repo for my specific needs.

```go
{{/*
Delete posts from yagpdb by using an emoji.
Trigger: Add reactions
*/}}

{{$emoji := "🗑️"}} {{/* emoji to delete yag posts */}}
{{$yrole := 1048764993925034065 }} {{/* roleID to require to delete yag messages */}}
{{$ma := 120 }} {{/* max age of posts allowed to be deleted, in seconds (discord max is 1 week) */}}
{{$del := 10 }} {{/* time before "you can't do that" post deletes itself, in seconds */}}

{{/* the message when you're not allowed to delete something */}}
{{$nope := (print .User.Mention ": \nSorry, but you can't delete that message, " .User "." ) }}

{{/* optional things to edit */}}
{{$la := 5}} {{/* number of messages to log when the emoji is used. Max 100 */}}

{{$modch := 970007312632795167 }} {{/* channel to log deletions - yag-cmd-log */}}
{{$color :=  11053224 }} {{/* color of modlog embed, in decimal */}}

{{$vidshare := 871735111127793674 }} {{/* vid share channel to not quote vpr message */}}

{{/* the message for the modlog - this will go in an embed */}}
{{$modmsg := (print " **" .User.Mention " used " $emoji " in <#" .Message.ChannelID ">** ([link](https://discord.com/channels/" .Guild.ID "/" .Message.ChannelID ")) at <t:" currentTime.Unix ">\n\n**User ID:** " .User.ID  )}}


{{/* Don't edit below */}}
{{$x := (currentTime.Sub .Message.Timestamp.Parse).Seconds|round|toInt}} {{/* Math to get seconds */}}

{{if and (eq .Reaction.Emoji.APIName $emoji) (eq .Message.Author.ID 204255221017214977) }}
{{if and (le $x $ma) (hasRoleID $yrole) (not .Message.Pinned) (not (reFind `(?i)(fruits basket)` .Message.Content) ) }}
	{{deleteMessage .Message.ChannelID  .Message.ID 1}}

	{{$logit := exec "logs" $la}}
	{{$logfooter := (joinStr "" "\n" "**" "[View Logs](" $logit ")" "**" )}}
	
	{{$split := (split .Message.Content "\n")}}
	{{$quoteit := (joinStr "> " $split)}}
	{{$qfooter := (print "\n\n**Deleted Message:**\n> " $quoteit ) }}
		
	{{if not .Message.Embeds}}
		{{$msg := (cembed "description" (print $modmsg $logfooter $qfooter ) "color" $color )}}
		{{sendMessage $modch $msg}}

	{{else if (or (eq .Channel.ID $vidshare) ((eq .Channel.ParentID $vidshare) ) )}}
		{{$user := (print .Message.ContentWithMentionsReplaced)}}
		{{sendMessage $modch (cembed "description" (print $modmsg $logfooter "\n\n**Deleted Message:**\nVPR Warning for " $user ". " ) "color" $color )}}

		
	{{else if and .Message.Embeds (ne .Channel.ID $vidshare) }}
		{{sendMessage $modch (cembed "description" (print $modmsg $logfooter ) "color" $color )}}
		{{sendMessage $modch (complexMessage "content" "\n**Deleted Message:**" "embed" (index .Message.Embeds 0) )}}
	
	{{else if not (hasRoleID $yrole)}}
		{{ $nr := " You don't have the right role."}}
		{{$y := (sendMessageRetID nil (print $nope $nr) ) }}
		{{deleteMessage nil $y $del}}
	{{else if (gt $x $ma) }}
		{{$nr := (print " Only messages less than " $ma " seconds old can be deleted." )}}
		{{$y := (sendMessageRetID nil (print $nope $nr) ) }}
		{{deleteMessage nil $y $del}}
	{{else if .Message.Pinned}}
		{{$nr := " Pinned messages cannot be deleted."}}
		{{$y := (sendMessageRetID nil (print $nope $nr) ) }}
		{{deleteMessage nil $y $del}}
	{{else if (reFind `(?i)(fruits basket)` .Message.Content)}}
		{{$nr := " We don't ghost ping Vicky. <:skeptical:759947442082021426>"}}
		{{$y := (sendMessageRetID nil (print $nope $nr) ) }}
		{{deleteMessage nil $y $del}}
	
	{{end}}
{{end}}
{{end}}
```
