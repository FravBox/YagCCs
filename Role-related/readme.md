# Role-related

### custom rolemenu.yag
 
 Gives a role on emoji add & takes away the role if they unreact.
 If they never unreact, role can be automatically removed with a delay (default is 1 week).

 ### give or take role cc.yag
 This works exactly like `/giverole` and `/takerole` except it will only ever work for one role you specify inside the CC. This is good for when you want mods to be able to add/remove one specific role, but not have the discord permissions to touch any of the others.      
 Example usage is like `-verify @user 2d`  duration is optional.

 This will also post in the modlog if you have that option turned on in YAGPDB's  dashboard under `Tools & Utilities -> Moderation`.


### Quick Reference
Role mention: `<@&1234>` where `1234` is the role ID.

#### Update rolemenu
`-rolemenu update (message id)`

#### Give someone multiple roles
```go
{{ $ids := cslice 1111 2222 3333 }}
 {{ range $ids }}
 {{- $silent := addRoleID . -}} 
 {{- end }}
 ```
 
 