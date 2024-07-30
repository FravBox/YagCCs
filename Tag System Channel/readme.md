# TAG SYSTEM CHANNEL - ABOUT
A tag system that uses a reference channel, buttons, and modals. Loosely based on [jo3-l](https://github.com/jo3-l)'s [Tag system](https://yagpdb-cc.github.io/tags/overview) on the YAGPDB-CC website.

Tags (sometimes called "snippets") are pre-formatted messages you can call at any time. They are specifically helpful for support servers where the same questions are asked frequently.

# Features
## No more text commands!
Create, manage, and search without having to remember the correct command formats
images: 1, 2, 3, 7, 5

## Partial/fuzzy search
Don't know what you're looking for? Get up to 29 partial matches
Images: 4, 6

## Reference Channel
Tired of forgetting what tags actually exist? All tags get posted to a reference channel. Read them all or click the "manage" button when you spot that one annoying typo.
Image 7

## Logging
Creating, editing, and deleting tags all gets logged in a separate channel of your choice.
image 8

## Role-based editing
Tag authors can always manage their own tags. But you can set a mod role that can edit any tags. There is also an admin role for the admin functions....

## Easy setup / admin functions
Once you've installed the custom commands to your dashboard, use `;admin` to initialize the system. 
Image 9

<ul><li> **Start** gets you started right away!</li>
<li>**Migrate Tags**      
Do you currently use [jo3-l](https://github.com/jo3-l)'s [Tag system](https://yagpdb-cc.github.io/tags/overview)? Convert all those tags to this system without losing them!     
<details><summary>Note about migration</summary>
- Migrating tags makes the admin the author of all tags migrated
- There is not an easy way to change the author of a tag (you would have to code a separate cc to do this for yourself)
- You must migrate ALL tags. If you stop partway through, the system will break and you will have to "delete all" before you can continue.
- Migration and "delete all" do not alter your old tags in any way.
</details></li>

<li>**Delete all**      
Don't like the system? Screwed it up royally somehow? This system cleans up after itself.</li>

<li>**Delete tags with no posts**    
Because we use the reference channel to keep track of our tags, deleting those posts can cause terror on the system. But don't worry - if you accidentally deleted a message, it's still there and we can recover it.</li></ul> 
image 10

## And of course... Calling tags anywhere
Can't have a tag system without being able to call the tags!
image 11

# HOW TO INSTALL
There are five custom commands (CCs). You need all five. I highly recommend making a CC group, naming it "Tag System," and putting all the commands in it.

Furthermore, to keep things organized, you should name each CC the same way it is named here - logging, modals, etc. This will make following the installation instructions much easier.

image 14

<ol><li>**If you have other CCs that use the `starts with ;` trigger, disable them.**     
Change the other CC triggers if possible. Running this system with other CCs of the same trigger may produce unwanted results in your server.</li>

<li>**Make a "Tag Reference" channel**    
This is where all of the tags will be posted on creation, as well as the buttons to interact with them. The systemw ill not work without this channel.    
- Change the channel permissions so everyone can see the channel and messages, but are unable to post in the channel.
- Make the first post in the channel yourself or with a bot, and save the message link. We will use it in the next step.</li>

<li>**Add `logging.yag` first and keep note of its CC ID.**     
image 12     
- Set the trigger to "none" in your dashboard.
- Inside the code, on line 5, change `$logch` to the ID of the channel you wish to post the tag logs. If you don't want any logs, keep it at `0`.     
(Note: I'd advise enabling logging at least for the first few tag actions so you know the system was installed properly)
- On line 8, put the message URL to the first post in your tag reference channel in `$first`.
- Line 10 and 14 are optional. If you don't like the thumbnail (in the footer) or embed color used for tags, change them here. Put your color in decimal form. You can find a color's decimal by using [Spycolor}(https://spycolor.com).    
<details><summary>A note about thumbnails</summary>
This system requires a thumbnail to function. It shows in the footer of all tags.    
image 13     
We need the image because we store the database key in its URL. This is what makes the "manage" button work in the tag reference channel.     
If you remove the image, the system will behave erradically and you may not be able to edit your tags.

If you don't like the current image and/or you wish to host it yourself, you can put any image URL in line 11 to replace it. However, the URL must be a DIRECT link to the image (it must end in the image extention, e.g. .jpg,.png, etc).

If you don't understand what any of this means, do not change the thumbnail URL.</details></li>

<li>**Add `modals.yag`**    
- On your dashboard, the trigger type is `modal submission` and the component custom ID regex is `^tag(m|s|e)-`
- Inside the code, on line 4, change `$log` to the CC ID of `logging.yag`. 
</li>

<li>**Add `admin.yag**    
- On your dashboard, the trigger type is `message component` and the regex is `^tagi-`
- Inside the CC, change line 10 `$admin` to the role ID you wish to have control of the entire tag system. This role will be able to run the admin functions (set up the system, migrate tags, delete everything) but cannot edit individual tags.
- Line 13 is an optional change. See the note about thumbnails in the `logging.yag` step.
- On line 16, change `$tch` to the ID of your "tag reference" channel. This is the channel with the first message you created in an earlier step. This channel shows all of your tags when they are created.
- On line 19, change `$logs` to the CC ID of `logging.yag`.
- Line 22 is an optional change if you want to change the color of tag embeds.</li>

<li>**Add `calling.yag`**    
- On your dashboard, the trigger type is `starts with` and the trigger is `;`
- Inside the CC on line 11, put the ID of the admin role from the previous step in `$admin`
- Line 14 and 17 are optional changes for the thumbnail and embed color. See the notes for these from the `logging.yag` step.
- Line 20 is an optional change. When YAGPDB cannot find a tag you are trying to call, it reacts with this emoji (and deletes the reaction 5 seconds later)
</li>

<li>**Add `buttons.yag`**    
- On your dashboard, the trigger type is `message component` and the regex is `^tag(e|s)-`
- Inside the CC on line 9, change `$staff` to the ID of the role you want to be able to manage anyt ag, regardless of its author. Tag authors will always be able to edit their own tags, regardless of roles.
- On line 12, put the CCID of the `logging.yag` command in `$log`
</li>

<li>**In discord, type `;admin` in any channel and click "start" to start the system.**     
- I highly recommend you run the admin functions in a channel that is NOT your tag reference channel.
- If you want to use any of the admin functions, read the admin message for instructions on how to use that function.
- If you create some tags and then later decide to migrate your old tags, this is possible. However, you should migrate as soon as possible because if any error should happen, the most likely outcome will be having to use the "delete all" function, which will delete the tags you created before migration.
</li></ol>

# Final Notes
- If you have problems, you can ping me in the YAGPDB support server: `@standardquip` or create an issue here on github
- Feel free to take these CCs and edit them to your own needs (provided you can read my code; apologies in advance)
- If you make a companion CC for this (such as enabling more admin functions or migrating from other systems) please let me know and I will link them here.
- I will fix problems/errors with this system but most likely will not add anything new. Almost all of the CCs are near the character limit and I don't have premium. If you want to optimize my code, I will accept PRs xD