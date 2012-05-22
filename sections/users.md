Users
=====

Get user
--------

* `GET /users/#{id}.xml` returns an existing user.

**Response:**

``` xml
<user>
  <id type="integer">1</id>
  <name>Jason Fried</name>
  <email-address>jason@37signals.com</email-address>
  <admin type="boolean">true</admin>
  <created-at type="datetime">2009-11-20T16:41:39Z</created-at>
  <type>Member</type>
  <avatar-url>https://asset0.37img.com/global/.../avatar.png</avatar-url>
</user>
```

Get self
--------

* `GET /users/me.xml` returns the user making the API request.

This end-point may be requested using the username and password, rather than the API token. This makes it easier for applications to obtain the typically-obscure API token on mobile platforms, where it is inconvenient to have to key in all 40 characters of the token.

**Response:**

``` xml
<user>
  <id type="integer">1</id>
  <name>Jason Fried</name>
  <email-address>jason@37signals.com</email-address>
  <admin type="boolean">true</admin>
  <created-at type="datetime">2009-11-20T16:41:39Z</created-at>
  <type>Member</type>
  <avatar-url>https://asset0.37img.com/global/.../avatar.png</avatar-url>
</user>
```
