Search
======

Looks through transcripts on this accounts.

For the full XML representation of messages, [check out the data reference](https://github.com/37signals/basecamp-classic-api/blob/master/sections/data_reference.md#message).


Search for term
---------------

* `GET /search/#{term}.xml` returns all the messages across all rooms on this account containing the supplied term.

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
    <starred>true</starred>
  </message>
  ...
</messages>
```
