# Reaction Tickets
VERY Basic "make a ticket when clicking a reaction" command.



## How To Use
Create a message for the ticket creation. Then add the reaction you want to use.     
You can add the reaction manually by yourself, or you can tell yag to add the reaction. It is recommended you have yag add the reaction. Use this code to do that:         
```go
{{/* add the reactions to the ticket post - you only use this once.
trigger: command     
The command can be literally anything. You can delete this cc after you use it the one time. */}}

{{$ch := 1234 }} {{/* channel ID of where the ticket reaction message is. */}}
{{$msg := 5678 }} {{/* Message ID of the reaction message */}}
{{$emoji := "📩" }} {{/* emoji you want to use for creating a ticket */}}
{{/* don't edit below */}}

{{addMessageReactions $ch $msg $emoji}}
{{deleteTrigger 1}}
```

Once the post is created and the emoji is added, take that information and edit the `reactionTicketPost.tmpl` command.      
The trigger for that command should be `reaction - added reactions only`. You should restrict its use to only the channel that post is in. 

You might also might want to add this to the ticket open message in the control panel:      
```go
{{sendMessage nil (joinStr "" "Welcome, " .User.Mention ".\n\nPlease describe the reasoning for opening this ticket. You can also upload screenshots.")}}
{{sleep 1}}

{{$closemsg := "Type `-ticket close` to leave the channel"}}
{{$close := sendMessageRetID nil $closemsg}}
{{sleep 1}}
{{pinMessage nil $close}}
```

This command tells you how to close a ticket and pins that message to the top of the ticket channel. I was unable to get closing tickets via emoji to work, so that's why this is here.
