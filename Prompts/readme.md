# Prompt System
I use this for creating prompts for videos. But this would work for writing or art servers, too. There is no prompt management. You can't delete prompts once they're submitted. The prompt list is extremely bare bones. Don't use this if you have malicious users.

Users type `-prompt text here` to submit their prompt. Yag collects them, randomizes them, and then posts a new prompt every 3 weeks.

![image](https://user-images.githubusercontent.com/20410737/178646991-63d2185d-298c-4626-91ed-6fe90273ea6d.png)

## dbsetprompt.tmpl
Trigger can be anything. Use it once to set up the system, then delete.

## prompt.tmpl
The main cc. Change the contents of `$thanksMessage`. This is what is posted when people submit new prompts.

## promptlist.tmpl
Optional. Lists the prompts.

## prompt-post.tmpl
504 hours is 3 weeks. Change the hourly interval in the trigger if you want to post prompts more or less often.    

`$channelToSend` ID of the channel prompts should be posted in.    
`$text` any text you want to display underneath the prompt (in the same embed).     
`$error` the text you want posted when there are no prompts left to post.

Nothing else should be changed.

