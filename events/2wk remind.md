This was bult to have Yag interact with Sesh.fyi event bot. 

Use:
1. Sesh makes an event post    
(at the least: an embed with a title and a unix timestamp)

2. You (a person) uses the `-deadline 1234` command.     
`1234` can be the event post's ID or URL.

3. This CC triggers. It will post the following:    
```
!remind [event embed title] [Date that is 7 days prior to event start date]

Click the bell icon to be DMed a week before [event embed title]!
<[message URL the embed is from]>
```

4. Sesh reacts to Yag's post with a bell emoji.    
(`!remind` is a command Sesh looks for.)

5. People click the emoji to be DMed a reminder of the event 7 days before it happens.


**Why this exists**    
My server posts a lot of deadlines for future competitions, and we needed an extra RSVP reminder at least a week in advance.     
More RSVP reminder options have been on the roadmap for Sesh for an entire year. I decided to abuse the remind function to get what I wanted in a workaround.     
Sesh finally updated to include a 1 week prior reminder. The CC below now does 2 weeks prior.

**THE CUSTOM COMMAND FOR YAG**

```
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
            
			{{$msg := sendMessage nil $msg1}}
			        
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
