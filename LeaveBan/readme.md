# LeaveBan     
If someone is muted or timed out and then leaves while they're still muted/timed out, they are banned.

Coded by Grafik, commissioned by me.

1. On the Yag dashboard, go to Tools & Utilities -> Moderation -> Mute    
Put this in the Mute DM area:    
```go
{{/* 
    Description: Ban user after leaving with mute || timeout
    Trigger Type: Mute feed
    Recommended Trigger: -
    Restrictions: -

    Author Tag: Grafik#5457
    Author ID: 473466385222205452
*/}}

{{if .Duration}}
    {{dbSetExpire .User.ID "noexit" "4u" (toInt .Duration.Seconds)}}
{{else}}
    {{dbSet .User.ID "noexit" "4u"}}
{{end}}
```

2. Put this in the unmute DM area:     
`{{dbDel .User.ID "noexit"}}`


3. On the Yag dashboard, go to Notifications & Feeds -> General.     
Put this in the leave message:     
```go
{{if (dbGet .User.ID "noexit")}}
    {{execAdmin (print "banid " .User.ID " leaving server after mod actions were taken")}}
    {{dbDel .User.ID "noexit"}}
{{end}}
```

4. If you want this applied to time outs as well, on the Yag dashboard, go to Tools & Utilities -> Moderation -> Timeout    
Put this in the Timeout DM area:     
```go
{{/* 
    Description: Ban user after leaving with mute || timeout
    Trigger Type: Timeout feed
    Recommended Trigger: -
    Restrictions: -

    Author Tag: Grafik#5457
    Author ID: 473466385222205452
*/}}

{{dbSetExpire .User.ID "noexit" "4u" (toInt .Duration.Seconds)}}
```

