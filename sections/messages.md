Messages
========

For the full XML representation of messages, [check out the data reference](https://github.com/37signals/campfire-api/blob/master/sections/data_reference.md#message).


Create message
--------------

* `POST /room/#{id}/speak.xml` sends a new message with the currently authenticated user as the sender.

The XML for the new message is returned on a successful request.

The valid types are:

* `TextMessage` (regular chat message),
* `PasteMessage` (pre-formatted message, rendered in a fixed-width font),
* `SoundMessage` (plays a sound as determined by the message, which can be `56k`, `bueller`, `crickets`, `dangerzone`, `deeper`,`drama`, `greatjob`, `horn`, `horror`,`inconceivable`,
`live`, `loggins`, `noooo`, `nyan`, `ohmy`, `ohyeah`, `pushit`, `rimshot`, `sax`, `secret`, `tada`, `tmyk`, `trombone`, `vuvuzela`, `yeah`, or `yodel`)
* `TweetMessage` (a Twitter status URL to be fetched and inserted into the chat)
If an explicit type is omitted, it will be inferred from the content (e.g., if the message contains new line characters, it will be considered a paste).

Newline characters are ignored for TextMessages. In order to include newlines inside of a PasteMessage, use this escape code: `&#xA;`

**Request:**

``` xml
<message>
  <type>TextMessage</type>
  <body>Hello</body>
</message>
```

**Response:**

    Status: 201 Created

``` xml
<message>
  <id type="integer">1</id>
  <body>Hello</body>
  <room-id type="integer">1</room-id>
  <user-id type="integer">2</user-id>
  <created-at type="datetime">2009-11-22T19:11:41Z</created-at>
  <type>TextMessage</type>
  <starred>false</starred>
</message>
```

Get recent messages
-------------------

* `GET /room/#{id}/recent.xml` returns a collection of upto 100 recent messages in the room. 

This endpoint accepts two additional optional parameters: `limit` to restrict the number of messages returned and `since_message_id` to get messages created after the specified message id.

**Response:**

``` xml
<messages type="array">
  <message>
    <created-at type="datetime">2010-04-15T11:03:08Z</created-at>
    <id type="integer">23</id>
    <room-id type="integer">1</room-id>
    <user-id type="integer">1</user-id>
    <body>Hello room!</body>
    <type>TextMessage</type>
    <starred>false</starred>
  </message>
  ...
</messages>
```


Highlight message
-----------------

* `POST /messages/#{message_id}/star.xml` highlights a message in the room's transcript

**Response:**

    Status: 200 OK


Unhighlight message
-------------------

* `DELETE /messages/#{message_id}/star.xml` removes a message highlight from the room's transcript

**Response:**

    Status: 200 OK
