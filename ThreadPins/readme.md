# Thread Pins

Allows the author of the first message in a thread to manage pins in the thread via post replies.

You do not need to edit anything for this to work!

**How to use it**    
The person who is the author of the very first post in a thread is considered the "Thread Author" (TAuthor / TA). The TA is the same person who created the thread unless they make a thread out of someone else's post (in that case, that post's author is the TA).     

If the TA wants to pin a post, they reply to the post with the word "pin". Yag will pin the post and delete all the mess in a few seconds.     
If the TA wants to unpin a post, reply to that post with "unpin" and Yag will do as told, cleaning up messages after.     
If someone other than the TA tries to manage pins, Yag posts that only thread starters can manage pins. Then deletes that message 5 seconds later.

![image](https://user-images.githubusercontent.com/20410737/178644114-e03e0181-5e6a-47ae-9ec9-4badf3caa263.png)     
![image](https://user-images.githubusercontent.com/20410737/178644253-29884577-969b-4ddf-a817-813d91f3a9e4.png)     
![image](https://user-images.githubusercontent.com/20410737/178644182-f5af6c92-f35e-4095-a7a3-9aa642890859.png)    
![image](https://user-images.githubusercontent.com/20410737/178644372-9f2ed8c7-f71f-4688-897d-aaa7b35dc81d.png)


## Part 1
Db entry expires in 6 months.

Regex: `\A`
```go
{{/* Yag saves the author of the message the thread was created from to the database. Necessary for pin cc. regex trigger \A */}}

{{if and .Channel.IsThread (not (dbGet .Channel.ID "ThreadAuthor"))}}
		{{ $TA1 := (getMessage .Channel.ParentID .Channel.ID).Author}}
		{{ $TA2 := dbSetExpire .Channel.ID "ThreadAuthor" $TA1 15770000}}
{{end}}
```

## Part 2     

Regex: `^(pin|unpin)`
```go
{{/* User replies to message with "pin" or "unpin" to manage message. Trigger type: regex. Trigger: ^(pin|unpin) */}}
{{$TAuthor := (dbGet .Channel.ID "ThreadAuthor").Value.ID}}

{{if and (.Channel.IsThread) (.Message.ReferencedMessage)}}
	{{if $TAuthor}}
		{{if eq .User.ID $TAuthor}}
			{{if eq (lower .Message.Content) "pin"}}
				{{if .Message.ReferencedMessage.Pinned}}
					{{$msg := sendMessageRetID nil "Message is already pinned."}}
					{{deleteMessage nil $msg 3}}
				{{else}}
					{{pinMessage nil .Message.ReferencedMessage.ID}}
				{{end}}
			{{else if eq (lower .Message.Content) "unpin"}}
				{{if not .Message.ReferencedMessage.Pinned}}
					{{$msg := sendMessageRetID nil "Message is already unpinned."}}
					{{deleteMessage nil $msg 5}}
				{{else}}
					{{unpinMessage nil .Message.ReferencedMessage.ID}}
					{{$msg := sendMessageRetID nil "Message unpinned."}}
					{{deleteMessage nil $msg 5}}
				{{end}}
			{{end}}
		{{else}}
		Only thread starters can manage thread pins.
		{{deleteResponse 5}}
		{{end}}
	{{else}}	
	Thread author not in database!
	{{end}}
{{deleteTrigger 2}}
{{end}}
```

Note about thread stuff: 
If the message in the main channel that says "X started a thread" ever gets deleted, the author comparison won't work. This is why I save it to db.

Also, message type 21 is thread creation message. But you can't use this to compare, because if anyone makes a thread via the plus icon in the message bar, instead of using a pre-existing message to create a thread from, it will not fire. 

**Optional Troubleshooting CC**     
Tells you who the Thread author is and if they're in the database.

![image](https://user-images.githubusercontent.com/20410737/178644441-7350ba1d-c882-4a08-9834-dda226f5fd28.png)


Command: `tauthor`
```go
{{$TAuthor := (dbGet .Channel.ID "ThreadAuthor").Value.ID}}

{{if and (.Channel.IsThread) ($TAuthor)}}
	{{(dbGet .Channel.ID "ThreadAuthor").Value.Username}} is the Thread Author(TA) and is in the database.
		{{if eq .User.ID $TAuthor}}
			You are the TA.
		{{else}}
			You are not the TA.
		{{end}}
{{else}}
TA is not in db or you're not in a thread.
{{end}}
```
