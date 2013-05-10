Campfire API
============

The Campfire API is implemented as vanilla XML/JSON over HTTP. You can explore the view part of the API (everything that's fetched with GET) through a regular browser. Using Firefox for this is particularly nice as it has a good, simple XML renderer (unlike Safari which just strips the tags and dumps the content).


Wrappers and example code
-------------------------

**Ruby**
* [Tinder](http://github.com/collectiveidea/tinder)
* [Broach](http://github.com/Manfred/broach)

**Python**
* [Pinder](http://github.com/rhymes/pinder)
* [pyfire](https://github.com/mariano/pyfire)
* [Camplight](https://github.com/mlafeldt/camplight)

**Objective-C**
* [HappyCamprFramework](https://github.com/blladnar/HappyCamprFramework/)

**PHP**
* [IceCube](http://labs.mimmin.com/icecube/)

**Java**
* [campfireclient](http://github.com/alandipert/campfireclient)

**C#**
* [ccnet.campfire.plugin](http://github.com/alexscordellis/ccnet.campfire.plugin)

Wrote your own API wrapper? Feel free to open a pull request and add to this list!


API Endpoints
-------------

* [Account](https://github.com/37signals/campfire-api/blob/master/sections/account.md)
* [Rooms](https://github.com/37signals/campfire-api/blob/master/sections/rooms.md)
* [Search](https://github.com/37signals/campfire-api/blob/master/sections/search.md)
* [Messages](https://github.com/37signals/campfire-api/blob/master/sections/messages.md)
* [Transcripts](https://github.com/37signals/campfire-api/blob/master/sections/transcripts.md)
* [Users](https://github.com/37signals/campfire-api/blob/master/sections/users.md)
* [Uploads](https://github.com/37signals/campfire-api/blob/master/sections/uploads.md)
* [Streaming](https://github.com/37signals/campfire-api/blob/master/sections/streaming.md)

(Hint: Press `t` to enable the file finder and type out the endpoint you need!)

Need a sample of each XML blob will look like? Check out the [Data Reference](https://github.com/37signals/campfire-api/blob/master/sections/data_reference.md).


Authentication
--------------

When you're using the API, it's always through an existing user in Campfire. There's no special API user. So when you use the API as "david", you get to see and work with what "david" is allowed to. Authenticating is done with an authentication token, which you'll find on the "My info" screen in Campfire.

When using the authentication token, you don't need a separate password. But since Campfire uses [HTTP Basic Authentication](http://www.ietf.org/rfc/rfc2617.txt), and lots of implementations assume that you want to have a password, it's often easier just to pass in a dummy password, like X.

Example using the authentication token and a dummy password through curl:

    curl -u 605b32dd:X https://sample.campfirenow.com/room/1.xml

    curl -u 605b32dd:X https://sample.campfirenow.com/room/2.json

Remember that anyone who has your authentication token can see and change everything you have access to. So you want to guard that as well as you guard your username and password. If you come to fear that it has been compromised, just change your regular password and the authentication token will change too.

The single exception to using the token for authentication is with the `/users/me.xml` endpoint, which may be accessed with the username and password of the authenticating user. The resulting XML will include (among other things) a `<api-auth-token>` element, containing the user's API token. This token can then be used for subsequent requests.

If you're making a public integration with Campfire for others to enjoy, you can also use OAuth 2. This allows users to authorize your application to use Campfire on their behalf without having to copy/paste API tokens or touch sensitive login info.

Read the [37signals API Authentication Guide](https://github.com/37signals/api/tree/master/sections/authentication.md) for more info on using OAuth.


Reading through the API
-----------------------

The Highrise API has two category of actions for reading: Get one, or get many. All these actions are done through an HTTP GET, which also means that they're all easily explorable through a browser as described above.

Here's a few examples of reading with curl:

    curl -u 605b32dd:X https://sample.campfirenow.com/rooms.xml

    curl -u 605b32dd:X https://sample.campfirenow.com/room/1.xml

If the read is successful, you'll get an XML response back along with the status code `200 OK`.


Writing through the API
-----------------------

Writing through the API is almost as easy as reading, but you can't explore it as easily through the browser. Regardless of your implementation language, though, using curl to play first is a great idea. It makes it very easy to explore the API and is perfect for small scripts too.

When you're writing through the API, you'll be sending XML or JSON to Campfire. You need to let the system know that fact by adding the appropriate content type header : `Content-type: application/xml` or `Content-type: application/json`. Then you just include the XML or JSON of the resource in the body of your request.

Here's a few examples creating new resources, first with the XML inline, second referencing the XML from a file:

    curl -u 605b32dd:X -H 'Content-Type: application/xml' \
    -d '<message><body>Hello</body></message>' https://sample.campfirenow.com/room/1/speak.xml

    curl -u 605b32dd:X -H 'Content-Type: application/xml' \
    -d @message.xml https://sample.campfirenow.com/room/1/speak.xml

Similarly, if you want to use JSON:

    curl -u 605b32dd:X -H 'Content-Type: application/json' \
    -d '{"message":{"body":"Hello"}}' https://sample.campfirenow.com/room/1/speak.json

The response to a succesful write operation is the status code `201 Created`. We also include the complete XML or JSON for the final resource in the response. This is because you can usually get away with creating a new resource with less than all its regular attributes.


Dealing with failure
--------------------

If a request fails, the error information is returned with the HTTP status code. For instance, if a requested record could not be found, the HTTP response might look something like:

    HTTP/1.1 404 The record could not be found
    Date: Thu, 16 Mar 2006 17:41:40 GMT
    ...

Note that, in general, if a request causes a new record to be created (like a new message, or to-do item, etc.), the response will use the `201 Created` status. Any other successful operation (like a successful query, delete, or update) will use a `200 OK` status code.

Rate limiting
-------------

You can perform up to 500 requests per 10 second period from the same IP address for the same account. If you exceed this limit, you'll get a `503 Service Unavailable` response for subsequent requests.  Check the `Retry-After` header to see how many seconds to wait before retrying the request.

SSL Usage
---------

A non-SSL request made against an account that has SSL enabled (and vice versa) will receive a "302 Found" response. The Location header will contain the correct URI.

If SSL is enabled for your account, ensure that you're using https. If it's not, ensure you're using http.


Documentation Conventions
-------------------------

To make things easier to understand, the following notation is used:

* `#{text}`: Indicates text that should be replaced by your own data
* `...`: Indicates content from the response has been elided for brevity in documentation. See the list of data responses at the end of the page for a full description of the format of that response type.


Help us make it better
----------------------

Please tell us how we can make this API better. If you have a specific feature request or if you found a bug, please [open a support ticket](http://help.37signals.com/tickets/new). Also, feel free to fork these docs and send a pull request with improvements!

To talk with us and other developers about the API, subscribe to the [37signals-api mailing list](http://groups.google.com/group/37signals-api).
