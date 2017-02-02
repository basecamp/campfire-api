Rooms
=====

The rooms API allows you to access information about any room under the account and lock/unlock the rooms.

Check out the data reference for a full XML representation of [rooms](https://github.com/37signals/campfire-api/blob/master/sections/data_reference.md#room) and [users](https://github.com/37signals/campfire-api/blob/master/sections/data_reference.md#user) .


Get rooms
---------

* `GET /rooms.xml` returns a collection of the rooms that are visible to the authenticated user.
* `GET /presence.xml` returns a collection of the rooms that the authenticated user is present in.

**Response:**

``` xml
<rooms type="array">
  <room>
    <id type="integer">1</id>
    <name>North May St.</name>
    <topic>37signals HQ</topic>
    <membership-limit type="integer">60</membership-limit>
    <full type="boolean">false</full>
    <open-to-guests type="boolean">true</open-to-guests>
    <active-token-value>#{ 4c8fb -- requires open-to-guests is true}</active-token-value>
    <updated-at type="datetime">2009-11-17T19:41:38Z</updated-at>
    <created-at type="datetime">2009-11-17T19:41:38Z</created-at>
  </room>
  ...
</rooms>
```


Get room
--------

* `GET /room/#{id}.xml` returns an existing room.

This endpoint also includes all the users currently inside the room.

**Response:**

``` xml
<room>
  <created-at type="datetime">2009-11-17T19:41:38Z</created-at>
  <id type="integer">1</id>
  <membership-limit type="integer">60</membership-limit>
  <name>North May St.</name>
  <topic>37signals HQ</topic>
  <updated-at type="datetime">2009-11-17T19:41:38Z</updated-at>
  <open-to-guests type="boolean">true</open-to-guests>
  <full type="boolean">false</full>
  <active-token-value>4c8fb</active-token-value>
  <users type="array">
    <user>
      <admin type="boolean">true</admin>
      <created-at type="datetime">2009-11-20T16:41:39Z</created-at>
      <email-address>jason@37signals.com</email-address>
      <id type="integer">1</id>
      <name>Jason Fried</name>
      <type>Member</type>
      <avatar-url>https://asset0.37img.com/global/.../avatar.png</avatar-url>
    </user>
    ...
  </users>
</room>
```


Update room
-----------

* `PUT /room/#{id}.xml` updates an existing room.

Only admins can rename a room, although any user (except guests) may set the topic. Omitting either tag results in that attribute being ignored. To remove a room topic, simply provide an empty `topic` tag.

**Request:**

``` xml
<room>
  <name>#{name}</name>
  <topic>#{topic}</topic>
</room>
```

**Response:**

    Status: 200 OK


Join room
---------

* `POST /room/#{id}/join.xml` joins the room for the current user

**Response:**

    Status: 200 OK


Leave room
----------

* `POST /room/#{id}/leave.xml` leaves the room for the current user

**Response:**

    Status: 200 OK


Lock room
---------

* `POST /room/#{id}/lock.xml` locks a room, preventing others from joining and stops transcripts from being logged

**Response:**

    Status: 200 OK


Unlock room
-----------

* `POST /room/#{id}/unlock.xml` unlocks a room, allowing others to join and re-enables transcripts

**Response:**

    Status: 200 OK
