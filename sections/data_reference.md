Data Reference
==============

The following sections describe the different data types used by the Campfire API.

Message
-------

``` xml
<message>
  <id type="integer">1</id>
  <room-id type="integer">1</room-id>
  <user-id type="integer">2</user-id>
  <body>Hello Room</body>
  <created-at type="datetime">2009-11-22T23:46:58Z</created-at>
  <type>
    #{TextMessage || PasteMessage || SoundMessage || AdvertisementMessage ||
      AllowGuestsMessage || DisallowGuestsMessage || IdleMessage || KickMessage ||
      LeaveMessage || SystemMessage || TimestampMessage || TopicChangeMessage ||
      UnidleMessage || LockMessage || UnlockMessage || UploadMessage
      ConferenceCreatedMessage || ConferenceFinishedMessage}
  </type>
  <starred>true</starred>
</message>
```

Room
----

``` xml
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
  <users type="array">
    ...
  </users>
</room>
```

Upload
------

``` xml
<upload>
  <id type="integer">1</id>
  <name>picture.jpg</name>
  <room-id type="integer">1</room-id>
  <user-id type="integer">1</user-id>
  <byte-size type="integer">10063</byte-size>
  <content-type>image/jpeg</content-type>
  <full-url>https://account.campfirenow.com/room/1/uploads/1/picture.jpg</full-url>
  <created-at type="datetime">2009-11-20T23:25:14Z</created-at>
</upload>
```

User
----

``` xml
<user>
  <id type="integer">1</id>
  <name>Jason Fried</name>
  <email-address>jason@37signals.com</email-address>
  <admin type="boolean">#{true || false}</admin>
  <created-at type="datetime">2009-11-20T16:41:39Z</created-at>
  <type>#{Member || Guest}</type>
  <avatar-url>https://asset0.37img.com/global/.../avatar.png</avatar-url>
</user>
```
