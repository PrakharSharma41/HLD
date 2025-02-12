
requirements:

real time messaging
group chat (user chat server sends message to message queue for each user)
last seen (last seen timestamp in user data)
read receipts
notification (use notification service to send notificaiton from message queue)
message synchronization across device (maintain counter for last read message per user)
online presence : use presence server(send heartbeat)

use websockets


Service discovery:

The primary role of service discovery is to recommend the best chat server for a client based on the criteria like geographical location, server capacity, etc. 
Apache Zookeeper [7] is a popular open-source solution for service discovery. 

Database to use:
tradeoff between consistency, availability, shard our database
we need more availability and less consistency for chat app
use nosql db with builtin sharding capabilities

• Key-value stores allow easy horizontal scaling.
• Key-value stores provide very low latency to access data.
• Relational databases do not handle long tail [3] of data well. When the indexes grow large, random access is expensive.

Database tables
users:
username, lastActive

messages:
message_id,user_id,text, media_url,conversation

conversation:
id, conversation_name, 

conversation_users:
conversation_id, user_id