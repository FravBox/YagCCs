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
