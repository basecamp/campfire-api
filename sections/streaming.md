Streaming
=========

The Streaming API allows you to monitor a room in real time. The authenticated user must already have joined the room in order to use this API.


Connections
-----------

Our servers will try to hold the streaming connections open indefinitely. However, API clients must be able to handle occasional timeouts or disruptions. Upon unexpected disconnection, API clients should wait for a few seconds before trying to reconnect.


Authentication
--------------

Authentication is done with a token, which you'll find on the "My Info" screen in Campfire. The streaming API doesn't support OAuth.

Formats
-------

The data stream is available in JSON or XML format. JSON is recommended.


API
---

* `GET https://streaming.campfirenow.com/room/#{id}/live.json` stream a single room’s messages.

The target host is always `streaming.campfirenow.com`.

**Response:**

``` json
{"room_id":1,"created_at":"2009-12-01 23:44:40","body":"hello","id":1,
 "user_id":1,"type":"TextMessage","starred":"true"}
{"room_id":1,"created_at":"2009-12-01 23:40:00","body":null,"id":2,
 "user_id":null,"type":"TimestampMessage","starred":"false"}
...
```


Examples
--------

Need to get started quickly with the Campfire Streaming API? Try one of our example scripts that use the [twitter-stream](http://github.com/voloko/twitter-stream) library or [YAJL Ruby C bindings](http://github.com/brianmario/yajl-ruby):

**twitter-stream**

``` ruby
# gem install twitter-stream
require 'twitter/json_stream'
 
token = 'xxx' # your API token
room_id = 111 # the ID of the room you want to stream
 
options = {
  :path => "/room/#{room_id}/live.json",
  :host => 'streaming.campfirenow.com',
  :auth => "#{token}:x"
}
 
EventMachine::run do
  stream = Twitter::JSONStream.connect(options)
 
  stream.each_item do |item|
    puts item
  end
 
  stream.on_error do |message|
    puts "ERROR:#{message.inspect}"
  end
 
  stream.on_max_reconnects do |timeout, retries|
    puts "Tried #{retries} times to connect."
    exit
  end
end
```

**YAJL**

``` ruby
# gem install yajl-ruby

require "uri"
require "yajl/http_stream"

token = 'xxx' # your API token
room_id = 111 # the ID of the room you want to stream

url = URI.parse("http://#{token}:x@streaming.campfirenow.com/room/#{room_id}/live.json")
Yajl::HttpStream.get(url) do |message|
  puts message.inspect
end
```
