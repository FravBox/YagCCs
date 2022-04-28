# Event Stuff

<details>
<summary>give role reskins</summary>

Things to edit:     
Large number is the roleID you want to assign. Otherwise, only edit the last line for the message yag posts when it gives the role.

**ELead**
```go
{{/* -elead @user duration */}}
{{/* assigns ELead */}}
 {{$args := parseArgs 2 (print "Please use the following format: `" .Cmd " <user> <duration>`")
    (carg "member" "Mention or ID")
    (carg "string" "Duration in (s, m, h, w etc)")}}
{{$v :=execAdmin "grole" ($args.Get 0).User "782386523634925598" (print "-d " ($args.Get 1))}}
{{ if $args.IsSet 0 }}
    {{ or ($args.Get 0).Nick ($args.Get 0).User.Username}} is now an ELead for {{($args.Get 1)}}!
{{ end }}
```

**Entrant / Enter**
```go
{{/*-enter @user duration */}}
{{/* assigns entrants */}}
 {{$args := parseArgs 2 (print "Please use the following format: `" .Cmd " <user> <duration>`")
    (carg "member" "Mention or ID")
    (carg "string" "Duration in (s, m, h, w etc)")}}
{{$v :=execAdmin "grole" ($args.Get 0).User "782386811473231880" (print "-d " ($args.Get 1))}}
{{ if $args.IsSet 0 }}
    {{ or ($args.Get 0).Nick ($args.Get 0).User.Username}} is now an entrant for {{($args.Get 1)}}!
{{ end }}
```

**EStaff**
```go
{{/* -staff @user duration */}}
{{/* assigns EStaff */}}
 {{$args := parseArgs 2 (print "Please use the following format: `" .Cmd " <user> <duration>`")
    (carg "member" "Mention or ID")
    (carg "string" "Duration in (s, m, h, w etc)")}}
{{$v :=execAdmin "grole" ($args.Get 0).User "782386637853949972" (print "-d " ($args.Get 1))}}
{{ if $args.IsSet 0 }}
    {{ or ($args.Get 0).Nick ($args.Get 0).User.Username}} is now EStaff for {{($args.Get 1)}}!
{{ end }}
```
</details>

<details>
<summary>Take Role reskins</summary>

Things to edit:      
Large number is roleID to take. Otherwise, only edit the last line for the message yag posts when it takes the role.

**ELead**
```go
{{/* -noelead @user */}}
{{/* removes ELead role */}}
 {{$args := parseArgs 1 (print "Please use the following format: `" .Cmd " <user>`")
    (carg "member" "Mention or ID")}}
{{$v :=execAdmin "rrole" ($args.Get 0).User "782386523634925598"}}
{{ if $args.IsSet 0 }}
    {{ or ($args.Get 0).Nick ($args.Get 0).User.Username}} is no longer an ELead.
{{ end }}
```

**Entrant / Exit**
```go
{{/* -exit @user */}}
{{/* removes entrant role */}}
 {{$args := parseArgs 1 (print "Please use the following format: `" .Cmd " <user>`")
    (carg "member" "Mention or ID")}}
{{$v :=execAdmin "rrole" ($args.Get 0).User "782386811473231880"}}
{{ if $args.IsSet 0 }}
    {{ or ($args.Get 0).Nick ($args.Get 0).User.Username}} is no longer an entrant.
{{ end }}
```

**EStaff**
```go
{{/* -nostaff @user */}}
{{/* removes EStaff role */}}
 {{$args := parseArgs 1 (print "Please use the following format: `" .Cmd " <user>`")
    (carg "member" "Mention or ID")}}
{{$v :=execAdmin "rrole" ($args.Get 0).User "782386637853949972"}}
{{ if $args.IsSet 0 }}
    {{ or ($args.Get 0).Nick ($args.Get 0).User.Username}} is no longer EStaff.
{{ end }}
```
</details>


# Enter Menu
3 files, 3 CCs, you need all 3 for this to work. **Make sure to limit this to a particular set of channels/roles; it's very easy to abuse**.     
In my server, verified users are allowed to create their own channels for events. If they want to easily ping people participating in their events, they ping a specific role. We created this menu for people to easily self-assign the role during events in order to create that ping list. 

The user submits `-entermenu`    
This creates and pins a message with a 🏆 reaction on the message. Anyone who uses that reaction is given a role ("entrant" - You need to change the name/role ID for your server).    
This role is automatically removed in 7 days, or if the user unreacts to the message. 


`entermenu1`   
You don't have to change anything

`entermenu2`   
Change `RoleIDToUse` to... the Role you want to give. (Could also work with a cslice I suppose)     
`TimeInSeconds` is how long to wait before removing the role if the user never un-reacts. By default it's 7 days.    
The Author ID refers to Yag specifically - don't change/delete this or it will run the enter menu any time anyone replies with a trophy emoji.   

`entermenu3`   
The `RoleIDToRemove` should be the same roleID(s) used in `entermenu2`.   
Again, Author ID refers to Yag specifically.

# 2wk Remind

Yag detects the event title and timestamp from a message, calculates what the date will be 14 days prior to that timestamp, and posts a `!remind` command for that week prior date. For use with Sesh.fyi. 

Use:     
1. Sesh makes an event post    
(at the least: an embed with a title and a unix timestamp)

2. You (a person) uses the `-deadline 1234` command.     
`1234` can be the event post's ID or URL.

3. This CC triggers. It will post the following:    
```
!remind [event embed title] [Date that is 14 days prior to event start date]

Click the bell icon to be DMed a week before [event embed title]!
<[message URL the embed is from]>
```

4. Sesh reacts to Yag's post with a bell emoji.    
(`!remind` is a command Sesh looks for.)

5. People click the emoji to be DMed a reminder of the event 14 days before it happens.


**Why this exists**    
My server posts a lot of deadlines for future competitions, and we needed an extra RSVP reminder at least a week in advance.     
More RSVP reminder options have been on the roadmap for Sesh for an entire year. I decided to abuse the remind function to get what I wanted in a workaround.     
Sesh finally updated to include a 1 week prior reminder in feb 2022. The CC below now does 2 weeks prior.

**THE CUSTOM COMMAND FOR YAG**

```go
{{/* Built by TheHolyWatermelon#0160 on commission by Vars#3616 
Trigger: Command: deadline
*/}}

{{if .CmdArgs}}
    {{$id := 0}}
    {{if $get := reFindAllSubmatches `https://(?:\w+\.)?discord(?:app)?\.com/channels\/(\d+)\/(\d+)\/(\d+)` (index .CmdArgs 0)}}
        {{$id = index $get 0 3}}
    {{else}}
        {{$id = index .CmdArgs 0 | toInt}}
    {{end}}
    {{if and ($e := (getMessage .Channel.ID $id).Embeds) $id}}
        {{$d := ""}}
        {{range (index $e 0 | structToSdict).Fields}}
            {{- if reFind `Time\s` ($k := print .) -}}
                {{- $d = reFind `\d+` $k | toInt -}}
            {{- end -}}
        {{end}}
        {{if gt (mult (sub $d 1210000)) currentTime.Unix}}
			{{$msg1 := print "!remind " (index $e 0 | structToSdict).Title (formatTime ($.UnixEpoch.Add (toDuration (mult (sub $d 604800) $.TimeSecond))) " Monday, Jan 02 at 15:04") "\n\nReact with 🔔 to be DMed **2 weeks before** " (index $e 0 | structToSdict).Title "!\nhttps://discord.com/channels/" $.Guild.ID "/" $.Channel.ID "/" $id ""}}

			{{$msg2 := print "React with 🔔 to be DMed **2 weeks before** " (index $e 0 | structToSdict).Title "!\nhttps://discord.com/channels/" $.Guild.ID "/" $.Channel.ID "/" $id ""}}
            
			{{$msg := sendMessageRetID nil $msg1}}
			{{sleep 5}}
			{{editMessage nil $msg $msg2}}
        
		{{else}}
            {{print "Output date is before current time"}}
        {{end}}
    {{else}}
        {{print "No embed attached to this message"}}
    {{end}}
{{else}}
    {{print "No ID or link provided"}}
{{end}}
{{deleteTrigger 5}}
```
