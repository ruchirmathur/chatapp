## Chatapp is a chat application that addresses the following use cases.

1. Logged in users should be able to chat with each other. 
2. Users should be able to chat in a group setting. 
    <!--
    2.1 Any limitation for Max users in a group
    2.2 Can a user leave a group?
    -->
3. Users should be able send text as well as photos and video messages. 
    <!-- 
    3.1 Only file extensions are validated for photo/video uploads? 
    3.2 Where and how long the files would be stored?
    3.3 Will there be a usage quota allocated for the user ?
    -->

## Non Functional Requirements

1. This system should be highly available and must work with low latency.
2. Messages must be retained for all the users.
   <!-- how long message will be retained for? -->

## Usage Pattern

The following usage patterns are just for reference and they do not correspond to an actual production application

1. Number of logged in users in a day - 1 million
2. Size of text message per user - 1 KB
3. Number of videos and photos shared per day - 1 million
4. Size of each photos/videos - 5 MB 
5. Total size of photos/videos - 5000 * 1000,000 = 5000,000,000 KB

## Resource Estimations

The following are just some resource estimations done based on the usage patterns provided

1. Each server serves - 8000 requests per day
2. Number of active users - 1000,000 users 
    <!-- 
     Number of active users would be more than users logged in a day, this number should be more than 1 million 
     -->
3. Total number of servers = Number of active users or the number of requests coming onto the servers/Number of requests that the server can serve - 1000,000/8000 = 125 servers
4. Total storage space = Total text size + Total photo/video size = 1000,000 * 1 + 1000,000 * 5000
5. Total network bandwidth = Number storage size/Number of seconds in a day =  5,001,000,000/86400 = 5788 

## System Components

The following system components are considered to design a chat application.

#### 1. Websocket servers
#### 2. Servers
#### 3. Load Balancers
#### 4. Cache 
#### 5. Database
#### 6. Content Distribution Network
#### 7. Blob Storage
#### 8. Messaging system

## System Design
 
### API Design

    Following API's are considered in the design.
 
    1. user API - This API will be used to retrieve the user information
      Request - userId
      
    2. writeMessage API - This API will be used to write messages to other users
      Request - fromUserid, toUserId, text, timestamp
      
    3. readMessage API - This API will be used to read the messages that a user has sent to another user
      Request - fromUserId, toUserId,timestamp
      
    4. writePhotoVideo API - This API is used to write Photos and Videos meta data into a daatastore and keep the photos and videos in a blob store.
      Request -  fromUserId, toUserId, videoUrl,photoUrl,timestamp
      
    5. readPhotoVideo  - This API is used to read photos meta data from the datastore and send appropriate photo content to the user from the blob store.
      Request - fromUserId, toUserId, timestamp
     
    6. groupMessage API
       <!--
        Can we make writeMessageAPI's touserId field as multivalued instead of new API for groupMessage API? 
        -->

### Database Design
     
   #### Table Design
     
    1. User - This table will contain the user related information.
       columns - user_id, first_name, last_name, email_addr
       
    2. Message - This table will contain the message related information
       columns - from_user_id, to_user_id, message, message_id, photo_url, photo_id, video_url,video_id, timestamp
       
   ##### Message Data 
   
   Since the messages sent by a user may not be read immediately, hence a database that supports eventually consistency is choosen.
       
   ##### User Data 
   
   This data can be kept in a relational store or a non relational store.
   
       
 ### Websocket Design
 
     Http Push and Http Pull are 2 technologies that can be used to send messages to users. In case of chat applications 
     there is generally  a need for a bidirectional transfer of data with low latency. For this purpose, Http Push 
     methodology is used. In Http Push methodology,websocket technology allows persistent connections to be opened between the
     clients and servers and this helps in reducing any latency that may be there between client and server.
     
 ### Caching Design
 
 
 ### Messaging Design
    
