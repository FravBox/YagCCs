# Introductions channel
This is a set of 3 commands that makes an introduction channel using buttons and modals (text input).

![image](https://github.com/FravBox/YagCCs/assets/20410737/25c14a90-3f2c-4ab0-9231-9ea85bd988a7)
![image](https://github.com/FravBox/YagCCs/assets/20410737/607f417f-90df-4498-90b1-968f9dd0e004)



# Features
- No more messing with roles or auto message deletes to make sure everyone only posts once
- Uses fancy buttons and modals (text inputs)
- If they already have an intro, the modal pre-fills with their previous intro text
- The system logs when someone creates, edits, or deletes their intro
- An optional companion command will also delete their intro when they leave the server

# Set up 
- Choose or make a channel for introductions and make a first post there.
- Make your intros channel viewable by everyone, but make it so no one (except you & YAGPDB) can post there.
- Create a new custom command group labeled "Intros" in the YAGPDB dashboard.
- Limit all the commands in this group to the intros channel.
- Copy the link to the first message in the intros channel and put it in `$first` in the `sticky.yag` command.
- Copy the channel ID for your intros channel and put it in `$ch` for all three commands.
- Add `sticky.yag`  as the first command, and take note of the CC ID.
- Edit `$sticky` in the other 2 commands so it uses the correct CC ID.
- Put the Channel ID of where you want intros logged in the following places:
 - `$log` in `components.yag`
 - `$jl` in `modal submission.yag`

- **To delete intros when a user leaves**, add `del intro on leave.yag` command to your leave message. Change `$modl` to the channel ID of your modlog.
- On the off-chance you used a previous version of this cc (before buttons were used), you will need to delete all the previous intro db entries or this won't work properly.

## That's it!
It should "just work"
