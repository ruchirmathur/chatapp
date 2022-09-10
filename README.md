## Chatapp is a chat application that addresses the following use cases.

1. Logged in users should be able to chat with each other.
2. Users should be able to chat in a group setting.
3. Users should be able send text as well as photos and video messages.

## Non Functional Requirements

1. This system should be highly available and must work with low latency.
2. Messages must be retained for all the users.

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
3. Total number of servers = Number of active users or the number of requests coming onto the servers/Number of requests that the server can serve - 1000,000/8000 = 125 servers
4. Total storage space = Total text size + Total photo/video size = 1000,000 * 1 + 1000,000 * 5000
5. 
