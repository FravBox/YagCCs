# ThreadPins      
Allows author of first post in a thread to manage the pinned messages in that thread

# LogCreation    
Pushes a message to a specific channel any time a thread is created - AKA logs thread creation.

# If you want to use both
You CAN use both if you want to, but it will create superfluous database entries. To only make one db entry per thread, go into `ThreadPins` and follow the instructions there for using both.

# Thread List     
(just an idea for now, no code yet)     
Use db entry from thread logging to create a list of threads for parent channel ID. Bonus points if it's only active threads (or can at least separate active from archived).
