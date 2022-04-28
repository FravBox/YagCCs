These are backups specifically for my server. You can reference them if you want, but they're not written to be easily edited.

**-dice**
```go
{{sendMessage nil  "You rolled 2d6" }}
{{execAdmin "roll 2d6"}}
```

**-noyag**
```go
{{/* Deletes Yag's last message */}}
	{{$silent := (execAdmin "clear 1 204255221017214977 -ma 5m -nopin")}}
	{{deleteTrigger 0}}

 

{{/* Sends to modlog */}}
	{{$modlog := 750544945474961448}}
	{{$log := execAdmin "logs 10"}}
	{{$msg := cembed "description" (joinStr "" "**" .User.Mention "** (ID: " .User.ID ") used `-noyag` in " .Channel.Mention  "\n([View Logs](" $log "))" )  "color" 16772608 }}

	{{sendMessage $modlog $msg}}
  ```

  **Regex: `(?i)\bupload\b`**
  ```go
  {{/* upload your amv auto emoji */}}
{{addReactions ":upload:828387371351277619"}}
```

**Revive Events Threads** - hourly interval - 144 `#upcoming`      
```go
{{/* Revives Events List threads every 6 days (144 hours) so they don't get archived and all the links will continue to work. */}}
{{$threads := cslice 949443466482573343 949442962511786024}}

{{range $threads}}
  {{- $id := sendMessageRetID . "Reviven"}}
  {{- deleteMessage . $id 1}}
{{end}}
```

**Revive Guides Threads** hourly interval - 23 - #rules and info     
```go
{{/* Revives threads every 23 hours so they don't get archived and all the links will continue to work. 
hourly interval - 23 - #rules and info
*/}}
{{$threads := cslice 947237113408155688 947229919895769108 947229349239738440 947229226220789811 947228770681634926 947212821517725706 947211336432091186 947205206456815687}}

{{range $threads}}
  {{- $id := sendMessageRetID . "Reviven"}}
  {{- deleteMessage . $id 1}}
{{end}}
```

**Auto-link threads**     
```go
{{/* regex trigger:
(?i)(\#)((how to (critique|report|bot|event|tag|musubi))|meetup)|channel */}}

{{/* Messages */}}
{{$report := cembed "description" "<#947212821517725706> or [click here](https://discord.com/channels/750541618389712896/947212821517725706/947315239521746956)"}}

{{$meetups := cembed "description" "<#947211336432091186> or [click here](https://discord.com/channels/750541618389712896/947211336432091186/947331114370990080)"}}

{{$critique := cembed "description" "<#947205206456815687> or [click here](https://discord.com/channels/750541618389712896/947205206456815687/947235453843701840)\n See also: <#947237113408155688> or [click here](https://discord.com/channels/750541618389712896/947237113408155688/947237116004421692)"}}

{{$musubi := cembed "description" "<#947237113408155688> or [click here](https://discord.com/channels/750541618389712896/947237113408155688/947237116004421692)\n See also: <#947205206456815687> or [click here](https://discord.com/channels/750541618389712896/947205206456815687/947235453843701840)"}}

{{$events := cembed "description" "<#947229349239738440> or [click here](https://discord.com/channels/750541618389712896/947229349239738440/947287143963836478)\n\n Quick links: **[Event creation link](https://sesh.fyi/dashboard/750541618389712896/events/create?channel_id=752317819873394780)** | [How to use Sesh](https://discord.com/channels/750541618389712896/947229349239738440/947289326717403196) | [Sesh DM options](https://discord.com/channels/750541618389712896/947229349239738440/947292925895770122) | [Set your event channel permissions](https://discord.com/channels/750541618389712896/947229349239738440/947296454467256411)"}}

{{$bots := cembed "description" "<#947229226220789811> or [click here](https://discord.com/channels/750541618389712896/947229226220789811/947264973564936224)\n or post `-helpme` in <#751106748676309043>\n\nSee also: <#947229919895769108> or [click here](https://discord.com/channels/750541618389712896/947229919895769108/947365648009408523)"}}

{{$tags := cembed "description" "<#947229919895769108> or [click here](https://discord.com/channels/750541618389712896/947229919895769108/947365648009408523)\n or post `;tag` in <#751106748676309043>\n Get <#750544674011349053> [here](https://discord.com/channels/750541618389712896/750544674011349053/947605706503249920)\n\n See also: <#947229226220789811> or [click here](https://discord.com/channels/750541618389712896/947229226220789811/947264973564936224)"}}

{{$channels := cembed "description" "<#947228770681634926> or [click here](https://discord.com/channels/750541618389712896/947228770681634926/947273349107683328)"}}

{{/* If conditions */}}

{{if (reFind `(?i)(\#)(how to) (critique)` .Message.Content)}}
	{{sendMessage nil $critique}}
{{end}}

{{if (reFind `(?i)(\#)(how to) (musubi)` .Message.Content)}}
	{{sendMessage nil $musubi}}
{{end}}

{{if (reFind `(?i)(\#)(how to) (report)` .Message.Content)}}
	{{sendMessage nil $report}}
{{end}}

{{if (reFind `(?i)(\#)(how to) (bot)` .Message.Content)}}
	{{sendMessage nil $bots}}
{{end}}

{{if (reFind `(?i)(\#)(how to) (event)` .Message.Content)}}
	{{sendMessage nil $events}}
{{end}}

{{if (reFind `(?i)(\#)(how to) (tag)` .Message.Content)}}
	{{sendMessage nil $tags}}
{{end}}

{{if (reFind `(?i)(/#)(meetup|meetup )(guideline|rule)` .Message.Content)}}
	{{sendMessage nil $meetups}}
	{{end}}

{{if (reFind `(?i)(/#)(channel)` .Message.Content)}}
	{{sendMessage nil $channels}}
	{{end}}
```