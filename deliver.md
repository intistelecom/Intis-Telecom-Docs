# Asynchronous delivery reports

To receive delivery reports asynchronously you have to implement an http server at your side.  
Please setup this URI in your web account.

The URL should handle GET request as follows:
http://your.host.com/dlr?message-id={message-id}&state={state}
* **message-id** id string returned to you when you sent the message
* **state** delivery state, it is a number 0..9. Please use the table below to interpret the state code.

| Message State | Value | Type | Description |
|---------------|-------|------|-------------|
| SCHEDULED | 0 | Intermediate | The message is scheduled. Delivery has not yet been initiated. A message submitted with a scheduled delivery time may return this state when queried. This value was added for V5.0 of SMPP and V3.4 and earlier MCs are likely to return ENROUTE for scheduled messages. |
| ENROUTE | 1 | Intermediate | The message is in enroute state. This is a general state used to describe a message as being active within the MC. The message may be in retry or dispatched to a mobile network for delivery to the mobile. |
| DELIVERED | 2 | Final | Message is delivered to destination The message has been delivered to the destination. No further deliveries will occur. |
| EXPIRED | 3 | Final | Message validity period has expired. The message has failed to be delivered within its validity period and/or retry period. No further delivery attempts will be made. |
| DELETED | 4 | Final | Message has been deleted. The message has been cancelled or deleted from the MC. No further delivery attempts will take place. |
| UNDELIVERABLE | 5 | Final | Message is undeliverable. The message has encountered a delivery error and is deemed permanently undeliverable. No further delivery attempts will be made. Certain network or MC internal errors result in the permanent non-delivery of a message. Examples of such errors would be an unknown subscriber or network error that indicated that the given destination mobile was denied SMS service or could not support SMS. |
| ACCEPTED | 6 | Final | Message is in accepted state (i.e. has been manually read on behalf of the subscriber by customer service) This state is used to depict intervention on the MC side. Sometimes a malformed message can cause a mobile to power-off or experience problems. The result is that all messages to that mobile may remain queued until the problem message is removed or expires. In certain circumstances, a mobile network support service or administrator may manually accept a message to prevent further deliveries and allow other queued messages to be delivered. |
| UNKNOWN | 7 | N/A | Message is in invalid state The message state is unknown. This may be due to some internal MC problem which may be intermediate or a permanent. This state should never be returned. A MC experiencing difficulties that prevents it from returning a message state, would use this state. |
| REJECTED | 8 | Final | Message is in a rejected state The message has been rejected by a delivery interface. The reasons for this rejection are vendor and network specific. No further delivery attempts will be made |
| SKIPPED | 9 | Final |  The message was accepted but not transmitted or broadcast on the network. A skipped message is one that was deliberately ignored according to vendor or network-specific rules. No further delivery attempts will be made. |


