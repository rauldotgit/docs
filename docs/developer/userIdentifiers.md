---
sidebar_position: 3
---

# User identifiers

In the world of ABRouter statistics exists multiple user identifiers. The temporary user id and user id.
A temporary user id is an identifier to use when you don't have a real user id like a record from MySQL `users` table. It can be session-id or device id. You can generate it when the user doesn't have the permanent user id. For example, you can put PHP uniqid() to session and use it to send all events within the current session until the exchange for the permanent user id.
At the moment, when you already have the permanent user id, you have to send it with a temporary user id to glue the user. Send it at least one time. There is no problem with sending it always. If you have any temporary user id, you can send it along with a permanent one.
These users will become equal in the ABRouter system after the first glue.
Each relationship between those users with the event will be calculated as +1 in the incremental display event type in the statistics.
