# Thread Logging

Sends a post to a specific channel any time a thread is created. Original code is a combination of my & Dei's efforts, but it was Dei's idea and ultimately her code so she gets the credit :)

I have logged the original command here, and at some point in the (hopefully) near future I will edit it to something I'd like to use that matches my other logs.

**If you want to use BOTH this and ThreadPins, do not use these cods and go to the ThreadPins folder instead.**

## Original.yag
Meant to mimic carlbot's logs, the only easily editable variable is the logging channel. Default db expiry is `15770000` which is 6 months.       
![image](https://user-images.githubusercontent.com/20410737/180127245-aa71b617-967b-4560-ad21-fce7a09707bb.png)

## Newer.yag
My version of the same code, user-friendly editable variables for logging channel, db expiry, and embed color.         
![image](https://user-images.githubusercontent.com/20410737/180127299-50b45a2a-69ad-4e21-8abb-6af555a20de1.png)


## About Database expiration
If someone posts in a thread past the database expiration, it will post a new log for the thread as if it were just created. You can make the db entry last for several years, but this is unecessary in most cases. Please adjust the time to your server's needs, so it expires some time after people normally stop using the threads.
