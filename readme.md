It is a Flask backend application.
It converts mp4 files into mp3.
It build up in microservice architecture

1) auth service (which check the authenticaton of user and validate using JWT)
2) gateway service (which act as entry point for client)
3) rabbitmq service (It is saving all the messages in a queue for Notification and Converter service)
4) Converter service (responsible for converting mp4 to mp3 file)
5) Notification service, it send an email to user for file conversion is done. 

Workflow: 
client -> gateway/login -> auth/login (MYSQL DB used for user details)
client -> gateway/upload -> auth/validate/ -> mp4 save to mongo db -> send message to rabbit mq
converter -> get message from rabbit mq -> convert the file -> save to mongo db -> send message to rabbit mq
notification -> receive message from rabbit mq -> get file id -> send email to the user
client -> gateway/download -> get mp3 from mongo db -> Download.

