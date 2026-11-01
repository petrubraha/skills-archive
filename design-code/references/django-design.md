# Django Design

## One Step per Line

Sending a Django Channels event to a user's WebSocket group:

```python
# Wrong behaviour.
send_to_ws_group(PrimitiveChat(request.user.id).ws_group, {"type": WebSocketEventType.SYSTEM_DISCONNECT})

# Correct behaviour.
user_id = request.user.id
user_chat = PrimitiveChat(user_id)
event = {"type": WebSocketEventType.SYSTEM_DISCONNECT}
send_to_ws_group(user_chat.ws_group, event)
```
