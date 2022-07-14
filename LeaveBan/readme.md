Commands that have something to do with mutes & time outs.

# LeaveBan     
If someone is muted or timed out and then leaves while they're still muted/timed out, they are banned.

Coded by Grafik, commissioned by me.

1. On the Yag dashboard, go to Tools & Utilities -> Moderation -> Timeout (and/or Mute)    
Put this in the Timeout and/or Mute DM area:    
```go
{{/* 
    Description: Create db after beign muted || timeouted
    Trigger Type: Mute && Timeout feed
    Recommended Trigger: -
    Restrictions: -

    Author Tag: Grafik#5457
    Author ID: 473466385222205452
*/}}

{{if .Duration}}
    {{dbSetExpire .User.ID "noexit" "4u" .Duration}}
{{else}}
    {{dbSet .User.ID "noexit" "4u"}}
{{end}}

{{/* your normal mute/timeout code */}}
```

2. On the Yag dashboard, go to Notifications & Feeds -> General.     
Put this in the leave message:     
```go
{{/* 
    Description: Ban user after leaving with mute || timeout
    Trigger Type: Leave feed
    Recommended Trigger: -
    Restrictions: -

    Author Tag: Grafik#5457
    Author ID: 473466385222205452
*/}}

{{if (dbGet .User.ID "noexit")}}
    {{execAdmin (print "banid " .User.ID " leaving server after mod actions were taken")}}
    {{dbDel .User.ID "noexit"}}

    {{/* your normal leave feed code :p */}}
{{end}}
```
