**Daisy Chain THREADS only**     
Regex: `.*`
```go
{{/* Sticky message for Daisy chain threads - 1min cooldown */}}

{{if .Channel.IsThread}}

{{/* 0 for per user, 1 for global */}}
{{$isGlobal := 0}}
{{/* name your cooldown name (anything works) */}}
{{$name := "Sticky Message Cooldown"}}
{{/* Length of the cooldown (in seconds) */}}
{{$lengthSec := 60}}

{{/* CREATING VARIABLES DO NOT TOUCH */}}
{{$id := 0}}
{{$key := joinStr "" "cooldown_" $name}}
{{if eq $isGlobal 0}}
{{$id = .User.ID}}
{{end}}


{{if dbGet (toInt64 $id) $key}} 
{{/* Code to execute when cooldown is active */}}
{{else}}
{{/* Create cooldown entry */}}
{{dbSetExpire (toInt64 $id) $key "cooldown" $lengthSec}}

{{/* Daisy chain threads sticky */}}

{{$message := cembed "title" "Don't talk in threads" "description" "Threads are for claiming and posting parts. \nPlease keep chatter to <#923034923684724788>. \n\n([Daisy Chain MEP Rules](https://discord.com/channels/750541618389712896/923034923684724788/923037349204590653)) \n" "color" 0xff6a00}}

{{/* do not edit below */}}
{{if $db := dbGet .Channel.ID "stickymessage"}}
	{{deleteMessage nil (toInt $db.Value) 0}}
{{end}}
{{$id := sendMessageRetID nil $message}}
{{dbSet .Channel.ID "stickymessage" (str $id)}}

{{end}}
{{end}}
```

**Everything Else**      
Regex: `/A`
```go
{{/* Sticky messages - Photosensitivity, daisy chain main, events */}}

{{/* Sticky message for Photosensitivity - 5min cooldown per user */}}
	{{if (eq .Channel.ID 944675758410965002)}}
		{{/* 0 for per user, 1 for global */}}
		{{$isGlobal := 0}}
		{{/* name your cooldown name (anything works) */}}
		{{$name := "photosensitive sm cd"}}
		{{/* Length of the cooldown (in seconds) */}}
		{{$lengthSec := 300}}

		{{/* CREATING VARIABLES DO NOT TOUCH */}}
		{{$id := 0}}
		{{$key := joinStr "" "cooldown1_" $name}}
		{{if eq $isGlobal 0}}
		{{$id = .User.ID}}


		{{if dbGet (toInt64 $id) $key}} 
		{{/* Code to execute when cooldown is active */}}
		{{else}}
		{{/* Create cooldown entry */}}
		{{dbSetExpire (toInt64 $id) $key "cooldown1" $lengthSec}}

		{{/* Photosensitivity sticky */}}

		{{$message := cembed "title" "This channel has strict rules" "description" "See the [pinned post](https://discord.com/channels/750541618389712896/944675758410965002/944677317874155570).\n Summarize the triggers that may be in your posted videos AND gifs. If you don't think they have any triggers, *you still have to state that.* \nSpoiler gifs if they might have triggers.\n **See the VPR website for a list of common triggers!**\nhttps://sashimi.khat.us/vpr\n\n**Malicious noncompliance will get you banned.** \n" "color" 0xff6a00}}

		{{/* do not edit below */}}
		{{if $db := dbGet .Channel.ID "stickymessage"}}
			{{deleteMessage nil (toInt $db.Value) 0}}
		{{end}}
		{{$id := sendMessageRetID nil $message}}
		{{dbSet .Channel.ID "stickymessage" (str $id)}}

		{{end}}
		{{end}}
	{{end}}


{{/* Sticky message for Daisy chain main - 10min cooldown per user */}}
	{{if (eq .Channel.ID 923034923684724788)}}
		{{/* 0 for per user, 1 for global */}}
		{{$isGlobal := 0}}
		{{/* name your cooldown name (anything works) */}}
		{{$name := "daisy chain main sm cd"}}
		{{/* Length of the cooldown (in seconds) */}}
		{{$lengthSec := 600}}

		{{/* CREATING VARIABLES DO NOT TOUCH */}}
		{{$id := 0}}
		{{$key := joinStr "" "cooldown2_" $name}}
		{{if eq $isGlobal 0}}
		{{$id = .User.ID}}
		{{end}}


		{{if dbGet (toInt64 $id) $key}} 
		{{/* Code to execute when cooldown is active */}}
		{{else}}
		{{/* Create cooldown entry */}}
		{{dbSetExpire (toInt64 $id) $key "cooldown2" $lengthSec}}

		{{/* Daisy chain threads sticky */}}

		{{$message := cembed "title" "Check the threads tab for the current MEP" "description" "Threads are to keep the MEP parts together. You can talk in the main channel. \nMake sure to post your MEP part both in the main channel and in the thread! \n\n([Daisy Chain MEP Rules](https://discord.com/channels/750541618389712896/923034923684724788/923037349204590653)) \n" "color" 0xff6a00}}

		{{/* do not edit below */}}
		{{if $db := dbGet .Channel.ID "stickymessage"}}
			{{deleteMessage nil (toInt $db.Value) 0}}
		{{end}}
		{{$id := sendMessageRetID nil $message}}
		{{dbSet .Channel.ID "stickymessage" (str $id)}}
		{{end}}
	{{end}}
	
	
{{/* Events sticky message */}}
	{{if (eq .Channel.ID 752317819873394780)}}
		{{ $avatar := "https://cdn.discordapp.com/attachments/750544650523246623/947397390887972933/kicking-musubi-w-text.png" }}

		{{$message := cembed "description" "**[CLICK HERE TO CREATE AN EVENT!](https://sesh.fyi/dashboard/750541618389712896/events/create?channel_id=752317819873394780)** \n[Read the pinned post](https://discord.com/channels/750541618389712896/752317819873394780/837090026226712576) for guides and ping list info.\n\n**View all events in <#836019207597588541>**" "color" 15559936 "thumbnail" (sdict "url" $avatar)}}

		{{/* do not edit below */}}
		{{if $db := dbGet .Channel.ID "stickymessage"}}
			{{deleteMessage nil (toInt $db.Value) 0}}
		{{end}}
		{{$id := sendMessageRetID nil $message}}
		{{dbSet .Channel.ID "stickymessage" (str $id)}}
	{{end}}
```