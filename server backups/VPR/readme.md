Regex: `.*`     
```go
{{/* Remind about vpr if no vpr mentioned */}}

{{/* Actual Message */}}
{{$add_vpr := cembed "title" "Flash warnings are required in this channel" "description" "Did you forget to add the [VPR](https://sashimi.khat.us/vpr/)?\n\n e.g. `VPR flashing`, `VPR glitch effects`, etc." "color" 0xff6a00 "thumbnail" (sdict "url" "https://media.discordapp.net/attachments/750544650523246623/947397390887972933/kicking-musubi-w-text.png") }}

{{/* Skip conditions */}}
{{$skip := false}}
{{if not (reFind `(?i)(youtube.com|youtu.be|vimeo.com|drive.google.com|streamable.com|frame.io|f.io)` .Message.Content)}}
    {{$skip := true}}

{{else if (reFind `(?i)(vpr|flash|flicker|glitch|shak|pattern|safe)` .Message.Content)}}
    {{$skip := true}}

{{/* Post the thing & add reaction */}}
{{else if not $skip}}
	{{$yagMsg := sendMessageRetID nil $add_vpr}}
	{{dbSetExpire 0 "yagMsg" (str $yagMsg) 604800}}
	{{sleep 1}}
	{{addMessageReactions nil $yagMsg "🗑️"}}
{{end}}
```

Added reactions only      
```go
{{/* Deletes VPR reminder on wastebin reaction */}}
{{$db := dbGet 0 "yagMsg"}}
{{$mid := toInt $db.Value}}

{{if and .ReactionAdded $db}}
	{{if and (eq $mid .Message.ID) (eq .Reaction.Emoji.Name "🗑️")}}
		{{deleteMessage nil $mid 1}}
		{{dbDel 0 "yagMsg"}}
			{{/* Logging */}}
				{{$modlog := 750544945474961448}}
				{{sleep 5}}
				{{$log := execAdmin "logs 5"}}
				{{$msg := cembed "description" (joinStr "" "**" .User.Mention "** (ID: " .User.ID ") used 🗑️ in " .Channel.Mention  "\n([View Logs](" $log "))" )  "color" 11053224 }}

				{{sendMessage $modlog $msg}}
	{{end}}
{{end}}
```

To delete the last db entry:      
`{{dbDel 0 "yagMsg"}}`      
`Deleted database entry`