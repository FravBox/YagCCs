# ThreadPins      
Allows author of first post in a thread to manage the pinned messages in that thread

# LogCreation    
Pushes a message to a specific channel any time a thread is created - AKA logs thread creation.

# If you want to use both
You CAN use both if you want to, but it will create superfluous database entries. To only make one db entry per thread, go into `ThreadPins` and follow the instructions there for using both.

# Thread List     
Got this working. Will adjust and make more official in the coming days. Triger can be any command. Yag will lag, so give it at least 5 seconds to respond.     
```go
{{/* lists top active threads as mentions. Must use "ThreadAuthor" db entry from ThreadPins code to work */}}

{{$amt := 10}} {{/* number of thread IDs to check. Archived threads count against the limit even if they aren't displayed in the output. Max 100. */}}

{{/* don't edit below */}}
{{$ch := ""}}
{{ $x := (dbTopEntries "ThreadAuthor" $amt 0) }}
{{range $x}}
{{- with (getChannelOrThread .UserID ) -}}
{{- print .Mention "\n" -}}
{{- $ch = joinStr " " $ch .ID -}}
{{- end -}}
{{- end}}
```

# Notes
**If you're using my code to help you make your own codes that involve threads, please read these notes**      
If the message in the main channel that says "X started a thread" ever gets deleted, the `.Message.Author` comparison won't work. This is why my CCs save the author to database.

Message type 21 is the thread creation message. But you can't use this in a CC to detect when a thread is created, because if anyone makes a thread via the plus icon in the message bar instead of using a pre-existing message to create a thread from, it will not fire. This is why my cc doesn't use message types.
