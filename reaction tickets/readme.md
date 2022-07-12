# Reaction Tickets
VERY Basic "make a ticket when clicking a reaction" command.     
Change `$ch` to reflect the channel ID and `$msg` to the message ID of the post you want people to react to.

Note: the included tickets system in YAGPDB must be enabled in order for this to work.

Create a message for the ticket creation. Then add the reaction you want to use:     
```go
{{/* add the reactions to the ticket post - you only use this once */}}

{{$ch := ChannelID}}
{{$msg := MessageID}}

{{addMessageReactions $ch $msg "📩"}}
{{deleteTrigger 1}}
```

**Actual reaction ticket CC**

On line 55 (of this document), change the roleID to whatever role you want to require in order for people to make a ticket this way.      
If you want everyone to be able to create a ticket, remove this part entirely: `(hasRoleID 750565698383773828)`

There's a 30min cooldown per user.
```go
{{/* if reaction on ticket post, open new ticket 
Trigger: added reactions only 
*/}}
{{$ch := 962877591050653726 }}
{{$msg := 962879864078221372 }}

{{/* 30min cooldown */}}
{{/* 0 for per user, 1 for global */}}
{{$isGlobal := 0}}
{{$name := "ticket creation"}}
{{/* Length of the cooldown (in seconds) */}}
{{$lengthSec := 1800}}

{{/* cooldown variables */}}
{{$id := 0}}
{{$key := joinStr "" "cooldown_" $name}}
{{if eq $isGlobal 0}}
{{$id = .User.ID}}
{{end}}


{{if dbGet (toInt64 $id) $key}} 
{{/* Code to execute when cooldown is active */}}

{{$ghost := sendMessageRetID nil .User.Mention }}
{{deleteMessage nil $ghost 0}}
{{$clm := sendMessageRetID nil "**You cannot create multiple tickets.**"}}
{{deleteMessage nil $clm 20}}

{{else}}
{{/* Create cooldown entry */}}
{{dbSetExpire (toInt64 $id) $key "cooldown" $lengthSec}}

{{/* ACTUAL TICKET CREATION */}}
{{if and (hasRoleID 750565698383773828) (eq .Message.ID $msg) (eq .Reaction.Emoji.Name "📩")}}
	{{$silent := exec "tickets open" (joinStr "" .User "")}}
{{end}}

{{sleep 5}}
{{deleteMessageReaction $ch $msg .Reaction.UserID "📩" }}

{{end}}
```

You might also might want to add this to the ticket open message in the control panel:      
```go
{{sendMessage nil (joinStr "" "Welcome, " .User.Mention ".\n\nPlease describe the reasoning for opening this ticket. You can also upload screenshots.")}}
{{sleep 1}}

{{$closemsg := "Type `-ticket close` to leave the channel"}}
{{$close := sendMessageRetID nil $closemsg}}
{{sleep 1}}
{{pinMessage nil $close}}
```
