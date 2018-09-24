# [WebSockets](https://en.wikipedia.org/wiki/WebSocket)
- **WebSocket**: enables ongoing, two-way conversation between a web client (ex.: a browser) and a web server
- Facilitates real-time data transfer to/from server
  - Made possible by:
    - Providing a standardized way for the server to send content to the client without being first requested by the client
    - Allowing messages to be passed back and forth while keeping the connection open

## [Action Cable](https://guides.rubyonrails.org/action_cable_overview.html)
- **Action Cable**: integrated WebSockets for Rails

### Publish/Subscribe
- **Pub/Sub**: message queue paradigm used by ActionCable, no need for specification of recipients (subscribers)

### Server-Side

- **Connection**: for every WebSocket, connection obj instantiated (instance of ```ApplicationCable::Connection```)

```rb
# Leeway/app/channels/application_cable/connection.rb
module ApplicationCable
  class Connection < ActionCable::Connection::Base

    identified_by :current_user # connection identifier, used to find specific connection later

    def connect
      self.current_user = find_current_user
    end

    protected
    def find_current_user
      current_user = User.find_by(session_token: env['rack.session'][:session_token])  # authentication of user elsewhere
      if current_user
        current_user  # ensure later retrieve all connections for same user
      else
        reject_unauthorized_connection
      end
    end
  end
end
```
<br/>

- **Channel**: encapsulates a logical unit of work
```rb
# Rails creates by default a parent class
# app/channels/application_cable/channel.rb
module ApplicationCable
  class Channel < ActionCable::Channel::Base
  end
end
```
```rb
# Create own channel classes
# app/channels/messages_channel.rb
class MessagesChannel < ApplicationCable::Channel
  def subscribed
    stream_from "chat-#{params['messageable_id']}:messages"
  end
end
```
