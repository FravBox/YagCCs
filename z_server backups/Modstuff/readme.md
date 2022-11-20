**-modhelp**
```go
{{/* sends message to #mod-commands */}}
{{$y := sendMessageRetID 786091493126438932 (print .User.Mention) }}
{{deleteMessage 786091493126438932 $y 5}}
{{deleteTrigger 0}}
```

**Regex: `^-(warn|kick|mute|report)`**     
`{{deleteTrigger 0}}`

**-modtoc**
```go{{/* Mod bot commands TOC */}}
{{$message := cembed 
    "title" (print "Mod Commands TOC" ) 
    "description" "[Intro](https://discord.com/channels/750541618389712896/786091493126438932/787084018998575134)\n[Muting](https://discord.com/channels/750541618389712896/786091493126438932/787104445984276511)\n[Warnings](https://discord.com/channels/750541618389712896/786091493126438932/787104564808515594)\n[Kicking & Banning](https://discord.com/channels/750541618389712896/786091493126438932/787105773859635220)\n[Snippet system](https://discord.com/channels/750541618389712896/786091493126438932/787106028457295913)\n[Event-related commands](https://discord.com/channels/750541618389712896/786091493126438932/787107479544528897)"
    "color" 0xff6a00
}}

{{sendMessage nil $message}}
```

**-mod** (pt 1)    
```go
{{/*
	Trigger: mod
	Trigger Type: Command

	Usage:
	mod @user

	Copyright (c): Black Wolf, 2021
	License: MIT
	Repository: https://github.com/BlackWolfWoof/yagpdb-cc/
*/}}

{{$prefix := index (reFindAllSubmatches `Prefix of \x60\d+\x60: \x60(.+)\x60` (exec "prefix")) 0 1}}
{{$args := parseArgs 1 (print $prefix "mod <UserID/Mention>") (carg "userid" "User")}}
{{if reFind `\d+` .StrippedMsg}}
	{{$user := userArg ($args.Get 0)}}
	{{$userid := $args.Get 0}}
	{{$users := "Unknown User"}}
	{{$usera := "https://cdn.discordapp.com/emojis/565142262401728512.png"}}
	{{if (userArg (index .CmdArgs 0))}}
		{{$userid = $user.ID}}
		{{$users = $user.String}}
		{{$usera = $user.AvatarURL "1024"}}
	{{end}}
	{{$x := sendMessageRetID nil (cembed
		"author" (sdict
			"name" (print $users " - Mod Panel")
			"icon_url" $usera)
		"description" "<a:bongoban:636572687124398081> - Ban, 👢 - Kick, <:servermute:711553322225500201> - Mute, 🔊 - Unmute, ❌ - Close Menu")}}
	{{/*Permission Check*/}}
	{{$var1 := split (index (split (exec "viewperms") "\n") 2) ", "}}
	{{/*Ban*/}}
	{{if (in $var1 "BanMembers")}}
		{{addMessageReactions nil $x "a:bongoban:636572687124398081"}}
	{{end}}
	{{/*Kick*/}}
	{{if (in $var1 "KickMembers")}}
		{{if $user}}
			{{addMessageReactions nil $x "👢"}}
		{{end}}
	{{end}}
	{{/*Mute*/}}
	{{if (in $var1 "ManageRoles")}}
		{{if $user}}
			{{addMessageReactions nil $x "servermute:711553322225500201" "🔊"}}
		{{end}}
	{{end}}
	{{addMessageReactions nil $x "❌"}}
	{{$v1 := dbSetExpire .User.ID (print .CCID "-" (randInt 10000) "del_message") (print "del" $x "-" .Message.ID) 300}}
	{{$v2 := dbSetExpire .User.ID "mod_rq_message" (print "mod" $x "-" $userid) 300}}
	{{deleteMessage nil $x 300}}
	{{deleteTrigger 300}}
{{else}}This ID is invalid and doesn't exist!{{end}}
```

**mod pt 2**

```go{{/*
	Trigger Type: Reaction (add)
	
	Copyright (c): Black Wolf, 2021
	License: MIT
	Repository: https://github.com/BlackWolfWoof/yagpdb-cc/
*/}}

{{$grab := ""}}
{{$call := dbGetPattern .User.ID "%message" 100 0}}
{{range $call}}
	{{if eq .UserID .User.ID}}
		{{$grab = print $grab " " .Value}}
	{{end}}
{{end}}
{{/*Delete Embed*/}}
{{$t11 := `del(?:(?P<MessageIDEmbed>\d{18})-(?P<MessageIDAuthor>\d{18}))`}}
{{range $call}}
	{{if and (eq $.Reaction.Emoji.Name "❌") (reFind $t11 .Value)}}
		{{$m := reFindAllSubmatches $t11 .Value}}
		{{if (reFind (str $.Reaction.MessageID) (str .Value))}}
			{{deleteMessage $.Reaction.ChannelID (index (index $m 0) 1) 0}}
			{{deleteMessage $.Reaction.ChannelID (index (index $m 0) 2) 0}}
			{{dbDelByID .UserID .ID}}
		{{end}}
	{{end}}
{{end}}
{{$e1 := `mod(?:(?P<MessageID>\d{18})-(?P<ModUserID>\d{18}))`}}
{{if and $call (reFind $e1 $grab)}}	{{$matches := reFindAllSubmatches $e1 $grab}}	{{$user := userArg (index (index $matches 0) 2)}}
	{{$users := "Unknown User"}}
	{{$usera := "https://cdn.discordapp.com/emojis/565142262401728512.png"}}
	{{$userid := toInt (index (index $matches 0) 2)}}
	{{if $user}}
		{{$users = $user.String}}
		{{$usera = $user.AvatarURL "1024"}}
	{{end}}
	{{/*Ban User*/}}
	{{if eq .Reaction.Emoji.Name "bongoban"}}
		{{range $call}}
			{{$grab = (print $grab " " .Value)}}
		{{end}}
		{{if (reFind `mod(?:(?P<MessageID>\d+)-(?P<ModUserID>\d+))` $grab)}}
			{{$matches := (reFindAllSubmatches `mod(?:(?P<MessageID>\d+)-(?P<ModUserID>\d+))` $grab)}}
			{{if eq (str .Reaction.MessageID) (str (index (index $matches 0) 1))}}
				{{editMessage nil .Reaction.MessageID (cembed
				"author" (sdict
					"name" (print $users " - Mod Panel")
					"icon_url" $usera)
				"description" "Option to ban <a:bongoban:636572687124398081> this user:\n🍏 - 1 Day\n🍎 - 1 Week\n🍊 - 2 Months\n🍋 - 4 Months\n🍌 - Permanent"
				"color" 0x77FF68)}}
				{{deleteAllMessageReactions nil .Reaction.MessageID}}
				{{addMessageReactions nil .Reaction.MessageID "🍏" "🍎" "🍊" "🍋" "🍌" "❌"}}
				{{dbSetExpire .User.ID "modmenu" "ban" 300}}
			{{end}}
		{{end}}
	{{end}}
	{{/*Kick User*/}}
	{{if eq .Reaction.Emoji.Name "👢"}}
		{{range $call}}
			{{if eq .UserID $.User.ID}}
				{{$grab = (print $grab " " .Value)}}
			{{end}}
		{{end}}
		{{if (reFind `mod(?:(?P<MessageID>\d+)-(?P<ModUserID>\d+))` $grab)}}
			{{$matches := (reFindAllSubmatches `mod(?:(?P<MessageID>\d+)-(?P<ModUserID>\d+))` $grab)}}
			{{if eq (str .Reaction.MessageID) (str (index (index $matches 0) 1))}}
				{{deleteAllMessageReactions nil (str .Reaction.MessageID)}}
				{{addMessageReactions nil (str .Reaction.MessageID) "❌"}}
				{{editMessage nil (str .Reaction.MessageID) (cembed
				"author" (sdict
					"name" (print $users " - Mod Panel")
					"icon_url" $usera)
				"description" (exec "kick" $userid "Kicked by Mod Panel")
				"color" 0x77FF68)}}
			{{end}}
		{{end}}
	{{end}}
	{{/*Mute User*/}}
	{{if eq .Reaction.Emoji.ID 711553322225500201}}
		{{range $call}}
			{{$grab = (print $grab " " .Value)}}
		{{end}}
		{{if (reFind `mod(?:(?P<MessageID>\d+)-(?P<ModUserID>\d+))` $grab)}}
			{{$matches := (reFindAllSubmatches `mod(?:(?P<MessageID>\d+)-(?P<ModUserID>\d+))` $grab)}}
			{{if eq (str .Reaction.MessageID) (str (index (index $matches 0) 1))}}
				{{editMessage nil (str .Reaction.MessageID) (cembed
				"author" (sdict
					"name" (print $users " - Mod Panel") 
					"icon_url" $usera)
				"description" "Option to mute <:servermute:711553322225500201> this user:\n🍏 - 5 Minutes\n🍎 - 10 Minutes\n🍊 - 20 Minutes\n🍋 - 1 Hour"
				"color" 0x77FF68)}}
				{{deleteAllMessageReactions nil (str .Reaction.MessageID)}}
				{{addMessageReactions nil (str .Reaction.MessageID) "🍏" "🍎" "🍊" "🍋" "❌"}}
				{{dbSetExpire .User.ID "modmenu" "mute" 300}}
			{{end}}
		{{end}}
	{{end}}
	{{/*Unmute User*/}}
	{{if eq .Reaction.Emoji.Name "🔊"}}
		{{range $call}}
			{{if eq .UserID .User.ID}}
				{{$grab = (print $grab " " .Value)}}
			{{end}}
		{{end}}
		{{if (reFind `mod(?:(?P<MessageID>\d+)-(?P<ModUserID>\d+))` $grab)}}
			{{$matches := (reFindAllSubmatches `mod(?:(?P<MessageID>\d+)-(?P<ModUserID>\d+))` $grab)}}
			{{if eq (str .Reaction.MessageID) (str (index (index $matches 0) 1))}}
				{{deleteAllMessageReactions nil (str .Reaction.MessageID)}}
				{{addMessageReactions nil (str .Reaction.MessageID) "❌"}}
				{{editMessage nil (str .Reaction.MessageID) (cembed
				"author" (sdict
					"name" (print $users " - Mod Panel")
					"icon_url" $usera)
				"description" (exec "unmute" $userid "Unmuted by Mod Panel")
				"color" 0x77FF68)}}
			{{end}}
		{{end}}
	{{end}}
	{{/*Checking for time emojis*/}}
	{{$result := 0}}{{$mute := "0"}}{{$ban := "0"}}
	{{if eq .Reaction.Emoji.Name "🍏"}}
		{{$result = 1}}{{$mute = "5m"}}{{$ban = "-d 1d"}}
	{{end}}
	{{if eq .Reaction.Emoji.Name "🍎"}}
		{{$result = 1}}{{$mute = "10m"}}{{$ban = "-d 1w"}}
	{{end}}
	{{if eq .Reaction.Emoji.Name "🍊"}}
		{{$result = 1}}{{$mute = "20m"}}{{$ban = "-d 2mo"}}
	{{end}}
	{{if eq .Reaction.Emoji.Name "🍋"}}
		{{$result = 1}}{{$mute = "1h"}}{{$ban = "-d 4mo"}}
	{{end}}
	{{if eq .Reaction.Emoji.Name "🍌"}}
		{{$result = 1}}{{$ban = "-d p"}}
	{{end}}
	{{if eq $result 1}}
		{{range $call}}
			{{if eq .UserID .User.ID}}
				{{$grab = (print $grab " " .Value)}}
			{{end}}
		{{end}}
		{{if (reFind `mod(?:(?P<MessageID>\d+)-(?P<ModUserID>\d+))` $grab)}}
			{{$matches := (reFindAllSubmatches `mod(?:(?P<MessageID>\d+)-(?P<ModUserID>\d+))` $grab)}}
			{{$author := (sdict "name" (print $users " - Mod Panel") "icon_url" $usera)}}
			{{if eq (str .Reaction.MessageID) (str (index (index $matches 0) 1))}}
				{{if eq (str (dbGet .User.ID "modmenu").Value) "mute"}}
					{{deleteAllMessageReactions nil (str .Reaction.MessageID)}}
					{{addMessageReactions nil (str .Reaction.MessageID) "❌"}}
					{{editMessage nil (str .Reaction.MessageID) (cembed
					"author" $author
					"description" (exec "mute" $userid $mute "Muted by Mod Panel")
					"color" 0x77FF68)}}
				{{end}}
				{{if eq (str (dbGet .User.ID "modmenu").Value) "ban"}}
					{{deleteAllMessageReactions nil (str .Reaction.MessageID)}}
					{{addMessageReactions nil (str .Reaction.MessageID) "❌"}}
					{{editMessage nil (str .Reaction.MessageID) (cembed
						"author" $author
						"description" (exec "ban" $userid $ban "Banned by Mod Panel")
						"color" 0x77FF68)}}
				{{end}}
			{{end}}
		{{end}}
	{{end}}
{{end}}
```