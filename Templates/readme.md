# Quick Reference

## .yag files
**Cooldown**     
Basic cooldown script. I don't know who originally made it.

**Cooldown-branching**      
Cooldown snippet from YAGPDB support server that has a branch to execute if you're still on cooldown.



## Random chance
written by shadow     
```go
{{$x := randInt 1 101}}
{{if le $x 10}}
    {{print "10% chance to get this message"}}
{{else}}
    {{print "90% chance for this"}}
{{end}}
```

## Update rolemenu
`-rolemenu update (message id)`

## Regex matching any mention 
`<@!?\d{17,}>`

## Give someone multiple roles
```go
{{ $ids := cslice 751451248091332758 751446179002318920 751450170323107862 }}
 {{ range $ids }}
 {{- $silent := addRoleID . -}} 
 {{- end }}
 ```
 
 ## Delete Trigger/response 
 `{{deleteTrigger 0}}`
`{{deleteResponse 0}}`

## Mentions
Role: `<@&773487900779348000>`      
Channel: `<#773487900779348000>`      
User: `<@773487900779348000>`       
`<@{{.User.ID}}>` Outputs a mention to the user that called the command and is the same as `{{.User.Mention}}`

## Delayed Ghost Ping
`{{$y := sendMessageRetID 786091493126438932 (print .User.Mention) }}`       
`{{deleteMessage 786091493126438932 $y 5}}`

## Send a DM
`{{$DMessage := "Your message here" }}`
`{{ sendDM $DMessage }}`