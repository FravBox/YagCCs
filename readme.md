# How To Use
Everything here assumes you can at least read basic code. I tell you what to edit for your server, but some are easier to use than others.

`server backups` and `old - reference only` aren't useful at all to outsiders.

<details>
<summary>Custom Report System</summary>

Updates a really old version of a report system previously found in the official Yag CC repo, because I didn't like how the [current version](https://yagpdb-cc.github.io/moderation/report-system/overview) works.

Includes my version (new) and the original (old) version.

</details>

<details>
<summary>Prompts</summary>

A very basic system that allows users to submit prompts for writing, art, etc. Yag collects them, randomizes them, and then posts them periodically.

</details>

<details>
<summary>ThreadPins</summary>

Allows the author of the first message in a thread to manage pins in the thread via post replies.

</details>

<details>
<summary>Events</summary>

- Some give and take role reskins

- Enter Menu     
    Posts something similar to a role menu that assigns a role on reaction and automatically removes the role in 7 days if the user never unreacts later.

- 2wk Remind     
    Yag detects the event title and timestamp from a message, calculates what the date will be 14 days prior to that timestamp, and posts a `!remind` command for that week prior date. For use with Sesh.fyi.

</details>

<details>
<summary>Misc</summary>

- Basic server stats     
- Improved bookmark command    
- Cooldown    
- Cooldown with branching    
- MessagePreview    
- Suggest   

</details>

<details>
<summary>Reaction tickets</summary>

VERY Basic "make a ticket when clicking a reaction" command.

</details>

<details>
<summary>Verification System</summary>

An entire verification system based on reacting with a specific emoji to a specific post. Heavily commented, customizable, and has some picture examples.    
This is probably my most user-friendly code in the repo.

Also has a nice join and leave message template.

</details>




P.S. ~~I don't know how to code at all.~~ I now BARELY know how to code, but most of these are frankensteined together from various publicly available snippets/templates, context clues, and Yag support lmao. So while these all work, they might not be the most efficient.

# Misc Notes

Official [Yag Docs](https://docs.yagpdb.xyz/): [CC templates](https://docs.yagpdb.xyz/reference/templates), [functions](https://docs.yagpdb.xyz/reference/templates/functions), [custom embed info](https://docs.yagpdb.xyz/others/custom-embeds)    
[Yag CC github](https://github.com/yagpdb-cc/yagpdb-cc)

Other Yag CC Gits:    
[BlackWolf](https://github.com/BlackWolfWoof/yagpdb-cc) | [Crenshaw](https://github.com/Crenshaw1312/Yagpdb-ccs) | [Altair](https://github.com/magratheaguide/altair)

# Quick Reference

**Update Rolemenu**    
`-rolemenu update (message id)`

**Regex matching any mention:** `<@!?\d{17,}>`


**Silently (no PM/msg) gives the user who did the trigger the role ID**    
`{{ $silent := (giveRoleID .user 751451248091332758)}}`

**the above command but for multiple roles at once**   
`{{ $ids := cslice 751451248091332758 751446179002318920 751450170323107862 }}    
{{ range $ids }}    
    {{- $silent := addRoleID  . -}}    
{{- end }}`


**Delete trigger/response seconds**    
`{{deleteTrigger 0}}`   
`{{deleteResponse 0}}`

**mention a role by id** (Must use `sendMessageNoEscape` or it won't actually ping the role)    
`<@&773487900779348000>`

**mention a channel by id**    
`<#773487900779348000>`

**mention a user by id**    
`<@773487900779348000>`    
`<@{{.User.ID}}>` Outputs a mention to the user that called the command and is the same as `{{.User.Mention}}`

**custom embeds**     
`-ce {"title": "hello", "description": "wew"}`

**Ping triggering user to a specific channel and then delete that message 5 seconds later** (a somewhat delayed ghost ping)    
`{{$y := sendMessageRetID 786091493126438932 (print .User.Mention) }}    
{{deleteMessage 786091493126438932 $y 5}}`

**Send a DM**     
`{{$DMessage := "Your message here" }}`     
`{{ sendDM $DMessage }}`
