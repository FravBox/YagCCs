Use trashcan emoji to delete any yag post. Doesn't quote the VPR messages to save space.       
Modified from the main repo for my specific needs.

```go
{{/*
Delete posts from yagpdb by using an emoji.
Trigger: Add reactions
*/}}

{{$emoji := "🗑️"}} {{/* emoji to delete yag posts */}}
{{$yrole := 750565698383773828 }} {{/* roleID to require to delete yag messages */}}
{{$ma := 30 }} {{/* max age of posts allowed to be deleted, in seconds (discord max is 1 week) */}}
{{$del := 10 }} {{/* time before "you can't do that" post deletes itself, in seconds */}}

{{/* the message when you're not allowed to delete something */}}
{{$nope := (print "Sorry, but you can't delete that message, " .User.Mention "." ) }}

{{/* optional things to edit */}}
{{$la := 5}} {{/* number of messages to log when the emoji is used. Max 100 */}}

{{$modch := 970007312632795167 }} {{/* channel to log deletions - yag-cmd-log */}}
{{$color :=  11053224 }} {{/* color of modlog embed, in decimal */}}

{{$vidshare := 871735111127793674 }} {{/* vid share channel to not quote vpr message */}}

{{/* the message for the modlog - this will go in an embed */}}
{{$modmsg := (print " **" .User.Mention " used " $emoji " in <#" .Message.ChannelID ">** at <t:" currentTime.Unix ">\n\n**User ID:** " .User.ID  )}}


{{/* Don't edit below */}}
{{$x := (currentTime.Sub .Message.Timestamp.Parse).Seconds|round|toInt}} {{/* Math to get seconds */}}

{{if and (eq .Reaction.Emoji.APIName $emoji) (eq .Message.Author.ID 204255221017214977) (not .Message.Pinned) (le $x $ma) (hasRoleID $yrole) }}
	{{deleteMessage .Message.ChannelID  .Message.ID 1}}

	{{$logit := exec "logs"}}
	{{$logfooter := (joinStr "" "\n" "**" "[View Logs](" $logit ")" "**" )}}
	
	{{$split := (split .Message.Content "\n")}}
	{{$quoteit := (joinStr "> " $split)}}
	{{$qfooter := (print "\n\n**Deleted Message:**\n> " $quoteit ) }}
		
	{{if not .Message.Embeds}}
		{{$msg := (cembed "description" (print $modmsg $logfooter $qfooter ) "color" $color )}}
		{{sendMessage $modch $msg}}
		
	{{else if and .Message.Embeds (ne .Channel.ID $vidshare) }}
		{{sendMessage $modch (cembed "description" (print $modmsg $logfooter ) "color" $color )}}
		{{sendMessage $modch (complexMessage "content" "\n**Deleted Message:**" "embed" (index .Message.Embeds 0) )}}
	
	{{else if (eq .Channel.ID $vidshare)}}
		{{sendMessage $modch (cembed "description" (print $modmsg $logfooter "\n\n**Deleted Message:**\nVPR Warning" ) "color" $color )}}
	{{end}}
	

	{{else if not (hasRoleID $yrole)}}
		{{ $nr := " You don't have the right role."}}
		{{$y := (sendMessageRetID nil (print $nope $nr) ) }}
		{{deleteMessage nil $y $del}}
	{{else if (or (gt $x $ma) (.Message.Pinned))}}
		{{$nr := " The message is pinned or too old to delete."}}
		{{$y := (sendMessageRetID nil (print $nope $nr) ) }}
		{{deleteMessage nil $y $del}}
{{end}}
```