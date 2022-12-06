# Explanation
These files are mostly the same as in the parent folder, but have much easier to read code and slightly different dict names. They are not backwards compatible with the other version of thread management.

If you wanted to use the emoji addon for example, you would need to rewrite the values it looks for in the code first.    
Here's the changes between the db entries:    
![image](https://user-images.githubusercontent.com/20410737/206024168-52ddb57e-3b63-4d3c-a94b-52a6eb445f91.png)

# Database Creation
`stripped down db creation.yag`    
This functions the same as the stripped down version in the parent folder.

# Automatic Thread List
`update on interval.yag`
Slightly improved version of the one in the parent folder.

Once you have some db entries for threads, you can make posts that automatically lists them all by category.
![image](https://user-images.githubusercontent.com/20410737/206024814-7fd6e270-8450-45b8-a920-04b21accf21a.png)

## Setup the Automatic thread list
**The VERY FIRST time you run this will take some setup. After that, it will just work by itself.**

- Go to or make a channel for your thread list    
- Have Yag submit some posts. You will need one post for every category you are tracking.     
(You may need to make a new cc. Anything can be the trigger. The cc should just be this line x however many posts you need)    
`{{sendMessage nil (cembed "description" "placeholder")}}`

In the list cc, replace "Category Name One" with the name of your first category. It is caps sensitive. Make sure you typed it correctly.

Go to the posts you just made in your thread list channel. Copy the message ID of the post you want to be your first category.    
Go back to the list cc. Replace the number to the right of your first category name (`1049748979472150589`) with the message ID you just copied.     

Repeat this for as many categories as you want to list. Delete whatever ones you don't use.

Once done, you can run the list cc for the first time, and it should update all of your placeholder posts.

**If there is an error about how the response is too long, you will have to split up the categories into multiple messages.**

I do not have a public example of how to do that. But the one I use in my server [is here](https://github.com/FravBox/YagCCs/blob/main/z_server%20backups/thread%20control/Auto%20updating%20thread%20list/part%202.yag). You will have to adjust the values it looks for so they match reisir's naming scheme.     

```go
{{$msgs := sdict
	"Vid Games"     (dict
    923031270563393557 1049138013852151939
    1020192256851980358 1049138014896525372
    923039490212241408  1049138032688762950
	)
}}
```
is
```go
{{$msgs := sdict
	"Category Name"     (dict
    [Parent Channel ID] [Message ID that Yag will edit the list into]
	)
}}
```

These modifications were made by Reisir#5441
