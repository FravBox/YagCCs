# Misc Notes

[Official CC Templates](https://docs.yagpdb.xyz/reference/templates) | [Yag CC github](https://github.com/jo3-l/yagpdb-cc) | [custom embed info](https://docs.yagpdb.xyz/others/custom-embeds)

**Update Rolemenu**    
-rolemenu update (message id)

**Regex matching any mention:** <@!?\d{17,}>


**Silently (no PM/msg) gives the user who did the trigger the role ID**    
{{ $silent := (giveRoleID .user 751451248091332758)}}

**the above command but for multiple roles at once**   
{{ $ids := cslice 751451248091332758 751446179002318920 751450170323107862 }}
{{ range $ids }}
    {{- $silent := addRoleID  . -}}
{{- end }}


**Delete trigger/response seconds**    
{{deleteTrigger 0}}   
{{deleteResponse 0}}

**mention a role by id**    
<@&773487900779348000>

**mention a channel by id**    
<#773487900779348000>

**mention a user by id**    
<@773487900779348000>    
<@{{.User.ID}}> Outputs a mention to the user that called the command and is the same as {{.User.Mention}}
