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
