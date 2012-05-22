Transcripts
===========

The Transcripts API lets you fetch all the messages for a specific day.

For the full XML representation of messages, [check out the data reference](https://github.com/37signals/basecamp-classic-api/blob/master/sections/data_reference.md#message).


Get messages for today
----------------------

* `GET /room/#{id}/transcript.xml` returns all the messages sent today to a room.

**Response:**

``` xml
<messages type="array">
  <message>
    <id type="integer">1</id>
    <body>Hello</body>
    <room-id type="integer">1</room-id>
    <user-id type="integer">2</user-id>
    <created-at type="datetime">2009-11-22T19:11:41Z</created-at>
    <type>TextMessage</type>
    <starred>false</starred>
  </message>
  ...
</messages>
```


Get messages for a specific date
--------------------------------

* `GET /room/#{id}/transcript/#{year}/#{month}/#{day}.xml` returns all the messages sent on a specific date to a room.

**Response:**

``` xml
<messages type="array">
  <message>
    <id type="integer">1</id>
    <body>Hello</body>
    <room-id type="integer">1</room-id>
    <user-id type="integer">2</user-id>
    <created-at type="datetime">2009-11-22T19:11:41Z</created-at>
    <type>TextMessage</type>
    <starred>false</type>
  </message>
  ...
</messages>
```
