New 1 part VPR message

```go
{{/* Remind about vpr if no vpr mentioned 
Trigger: regex .* */}}

{{/* Actual Message */}}
{{$add_vpr := cembed "title" (print .User ", Flash warnings are required in this channel") "description" "Did you forget to add the [VPR](https://sashimi.khat.us/vpr/)?\n\n e.g. `VPR flashing`, `VPR glitch effects`, etc." "color" 0xff6a00 "thumbnail" (sdict "url" "https://media.discordapp.net/attachments/750544650523246623/947397390887972933/kicking-musubi-w-text.png") }}

{{/* Skip conditions */}}
{{$skip := false}}
{{if not (reFind `(?i)(youtube.com|youtu.be|vimeo.com|drive.google.com|streamable.com|frame.io|f.io)` .Message.Content)}}
    {{$skip := true}}

{{else if (reFind `(?i)(vpr|flash|flicker|glitch|shak|pattern|safe)` .Message.Content)}}
    {{$skip := true}}

{{/* Post the thing & add reaction */}}
{{else if not $skip}}
	{{$yagMsg := sendMessageRetID nil (complexMessage "content" (print .User.Mention) "embed" $add_vpr )}}
	{{addMessageReactions nil $yagMsg "🗑️"}}
{{end}}
```
