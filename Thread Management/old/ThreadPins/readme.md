# Thread Pins

Allows the author of the first message in a thread to manage pins in the thread via post replies.

You must add both CCs - Part 1 & Part 2. You do not need to edit anything inside them for them to work. 

## How to use it

**You need 2 custom commands for this to work - Part1 and Part2.**       
The person who is the author of the very first post in a thread is considered the "Thread Author" (TAuthor / TA). The TA is the same person who created the thread unless they make a thread out of someone else's post (in that case, that post's author is the TA).     

If the TA wants to pin a post, they reply to the post with the word "pin". Yag will pin the post and delete all the mess in a few seconds.     
If the TA wants to unpin a post, reply to that post with "unpin" and Yag will do as told, cleaning up messages after.     
If someone other than the TA tries to manage pins, Yag posts that only thread starters can manage pins. Then deletes that message 5 seconds later.

![image](https://user-images.githubusercontent.com/20410737/178644114-e03e0181-5e6a-47ae-9ec9-4badf3caa263.png)     
![image](https://user-images.githubusercontent.com/20410737/178644253-29884577-969b-4ddf-a817-813d91f3a9e4.png)     
![image](https://user-images.githubusercontent.com/20410737/178644182-f5af6c92-f35e-4095-a7a3-9aa642890859.png)    
![image](https://user-images.githubusercontent.com/20410737/178644372-9f2ed8c7-f71f-4688-897d-aaa7b35dc81d.png)


## Part 1
**If you want to use ONLY ThreadPins:**         
Copy the code in `Part1-pins_only.yag`       
Trigger type: Regex, `\A`      
There is only one (optional) variable to change. It's when the database entry expires. The default is 6 months. If your thread is revived after db expiry, whoever revived it becomes the new thread author and can manage pins.

**If you want to use BOTH ThreadPins AND Thread creation logs:**       
Copy the code in `Part1-both.yag`      
Trigger type: Regex, `\A`    
You MUST change the value in `$ch` so it reflects where you want the log message posted. The other values are optional, and control when the db entry expires and the color of the embed. Thew default db expiry is in 6 months.      
If the thread is revived after the db expires, the log message will be sent again as if the thread were just created, and whoever revived the thread becomes the new thread author and can manage pins.

**Only use one of the `Part1`s!**

## Part 2     
Copy the `Part2.yag` code.      
Trigger type: Regex, `^(pin|unpin)`

There is only one (optional) thing to customize here. That is how many seconds before all the messages are cleaned. By default it's 5.


## Optional Troubleshooting CC     
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
