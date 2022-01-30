# Sticky posts
Just backups of my sticky posts.

Regex trigger: `.*`      
Make sure to restrict it to only the channel with the sticky post.

### Daisy Chain Threads
This will only fire in threads of the main channel and not the main channel itself.
```go
{{if .Channel.IsThread}}

{{/* Sticky message for Daisy chain threads */}}
{{$message := cembed "title" "Don't talk in threads" "description" "Threads are for claiming and posting parts. \nPlease keep chatter to <#923034923684724788>. \n\n([Daisy Chain MEP Rules](https://discord.com/channels/750541618389712896/923034923684724788/923037349204590653))" "color" 0xff6a00}}

{{/* do not edit below */}}
{{if $db := dbGet .Channel.ID "stickymessage"}}
	{{deleteMessage nil (toInt $db.Value) 0}}
{{end}}
{{$id := sendMessageRetID nil $message}}
{{dbSet .Channel.ID "stickymessage" (str $id)}}

{{end}}
```

### FAQ TOC
```go
{{/* FAQ TOC */}}
{{ $avatar := (joinStr "" "https://cdn.discordapp.com/attachments/750544650523246623/750756266737008760/kicking-sashimi.png") }}
{{$message := cembed 
    "title" (joinStr "" "Welcome to AMV Sashimi" ) 
    "description" "Read the <#750544650523246623>. Optionally, you can self-assign some <#750544674011349053>.\nIf you have any problems verifying, please post here.\nOtherwise, this channel also functions as an FAQ for the server.\nThis message will always appear last in this channel."
    "color" 0xff6a00
    "fields" (cslice 
		(sdict "name" "Server" "value" "Invite Link: https://discord.gg/F22nTuU \n [Channel List](https://discord.com/channels/750541618389712896/750544616553578527/784667270714228757)" "inline" false)
        (sdict "name" "Events" "value" "[Hosting/announcing events](https://discord.com/channels/750541618389712896/750544616553578527/784667405938589747) \n[Make an event channel & assign staff](https://discord.com/channels/750541618389712896/750544616553578527/784667543579000832) \n[Event participants: temporary (24hr) or manual assignment](https://discord.com/channels/750541618389712896/750544616553578527/784667628324782080) \n[Commands available in event channels](https://discord.com/channels/750541618389712896/750544616553578527/784667721076965386)" "inline" false) 
        (sdict "name" "Bot Commands" "value" "[Command list part 1](https://discord.com/channels/750541618389712896/750544616553578527/784671478913171466) \nHelp, reminders, suggestions, snippets \n[Command list part 2](https://discord.com/channels/750541618389712896/750544616553578527/784672908281905162) \nRoles, current time, polls, events" "inline" false)
(sdict "name" "Available Snippets" "value" "[Current snippet list](https://discord.com/channels/750541618389712896/750545021333274707/784673636287381504)\n(Note: You must be verified to view the snippet list)" "inline" false)
    ) 
    "thumbnail" (sdict "url" $avatar) 
}}


{{/* do not edit below */}}
{{if $db := dbGet .Channel.ID "stickymessage"}}
	{{deleteMessage nil (toInt $db.Value) 0}}
{{end}}
{{$id := sendMessageRetID nil $message}}
{{dbSet .Channel.ID "stickymessage" (str $id)}}
```

### Roles TOC
```go
{{/* Roles TOC */}}
{{$message := cembed "title" "Role Menus" "description" "Self-assign these optional roles at any time by reacting to the posts with the proper emoji. \n\n[Editing Programs](https://discord.com/channels/750541618389712896/750544674011349053/750552851914162297) \n[Operating Systems](https://discord.com/channels/750541618389712896/750544674011349053/750553222367936522) \n[AMV Types](https://discord.com/channels/750541618389712896/750544674011349053/750555509232369695) \n[Ping Lists](https://discord.com/channels/750541618389712896/750544674011349053/750557466520977482) \n[Username Colors](https://discord.com/channels/750541618389712896/750544674011349053/750566516994473984) \n[Pronouns](https://discord.com/channels/750541618389712896/750544674011349053/750760709888933921) \nCountries - [1](https://discord.com/channels/750541618389712896/750544674011349053/751460177659559936) | [2](https://discord.com/channels/750541618389712896/750544674011349053/752182029273268294)" "color" 0xff6a00}}

{{/* do not edit below */}}
{{if $db := dbGet .Channel.ID "stickymessage"}}
	{{deleteMessage nil (toInt $db.Value) 0}}
{{end}}
{{$id := sendMessageRetID nil $message}}
{{dbSet .Channel.ID "stickymessage" (str $id)}}
```
