Account
=======

The account API is currently just for reading, not writing. Any authenticated user has access.

Get account
-----------

* `GET /account.xml` returns info about the current account.

This endpoint includes:

* account id, subdomain, and name
* plan name (max, plus, etc.)
* owner’s user ID
* time zone in [tz format](http://en.wikipedia.org/wiki/Zone.tab)
* total storage used in bytes
* creation and last-update timestamps

**Response:**

``` xml
<account>
  <id type="integer">1</id>
  <name>Your Company</name>
  <subdomain>yourco</subdomain>
  <plan>premium</plan>
  <owner-id type="integer">#{user_id of account owner}</owner-id>
  <time-zone>America/Chicago</time-zone>
  <storage type="integer">17374444</storage>
  <created-at type="datetime">2011-01-12T15:00:00Z</created-at>
  <updated-at type="datetime">2011-01-12T15:00:00Z</updated-at>
</account>
```
