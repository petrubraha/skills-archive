# Django Design

## One Step per Line

Sending a Django Channels event to a branch's kitchen display group:

```python
# Wrong behaviour.
async_to_sync(channel_layer.group_send)(KitchenDisplay(order.branch_id).group_name, {"type": "order.confirmed", "order_id": order.id})

# Correct behaviour.
branch_id = order.branch_id
kitchen_display = KitchenDisplay(branch_id)
event = {"type": "order.confirmed", "order_id": order.id}
send_group_event = async_to_sync(channel_layer.group_send)
send_group_event(kitchen_display.group_name, event)
```
