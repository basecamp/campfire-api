Uploads
=======


Create upload
-------------

* `POST /room/#{id}/uploads.xml` uploads a file to the room.

POST a multipart/form-data request body (RFC 2388). The file parameter must be named `upload`.

**Request:**

    Content-Type: multipart/form-data; boundary=---------------------------XXX

    Content-Length: 8922

    -----------------------------XXX
    Content-Disposition: form-data; name="upload"; filename="me.jpg"
    Content-Type: image/jpeg
    ...

**Response:**

    Status: 201 Created

``` xml
<upload>
  <byte-size type="integer">8922</byte-size>
  <content-type>image/jpeg</content-type>
  <created-at type="datetime">2009-11-20T23:26:51Z</created-at>
  <id type="integer">1</id>
  <name>me.jpg</name>
  <room-id type="integer">1</room-id>
  <user-id type="integer">1</user-id>
  <full-url>https://account.campfirenow.com/room/1/uploads/1/me.jpg</full-url>
</upload>
```

Get uploads
-----------

* `GET /room/#{id}/uploads.xml` returns a collection of upto 5 recently uploaded files in the room.

**Response:**

``` xml
<uploads type="array">
  <upload>
    <byte-size type="integer">135</byte-size>
    <content-type>application/octet-stream</content-type>
    <created-at type="datetime">2009-11-20T23:26:51Z</created-at>
    <id type="integer">1</id>
    <name>char.rb</name>
    <room-id type="integer">1</room-id>
    <user-id type="integer">1</user-id>
    <full-url>https://account.campfirenow.com/room/1/uploads/4/char.rb</full-url>
  </upload>
  ...
</uploads>
```


Get upload
----------

* `GET /room/#{id}/messages/#{upload_message_id}/upload.xml` returns the upload object related to the supplied upload message id.

**Response:**

``` xml
<upload>
  <byte-size type="integer">135</byte-size>
  <content-type>application/octet-stream</content-type>
  <created-at type="datetime">2009-11-20T23:26:51Z</created-at>
  <id type="integer">1</id>
  <name>char.rb</name>
  <room-id type="integer">1</room-id>
  <user-id type="integer">1</user-id>
  <full-url>https://account.campfirenow.com/room/1/uploads/4/char.rb</full-url>
</upload>
```
