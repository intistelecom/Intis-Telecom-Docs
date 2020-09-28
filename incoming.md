# Asynchronous incoming messages

## Server requirements

To receive incoming messages asynchronously you have to implement an http server at your side.  
Please setup this URI in your web account.

<ins>The URI should handle POST request as follows:</ins>  
**URI:** http://your.icoming/script/uri   
**Content-type:** application/json  
**Body payload:**  

```javascript 
{
    "originatingAddress": "11234567123",
    "destinationAddress": "381233452345",
    "segmentedMessage" : {
        "message": "message content string",
        "msgRefNum": 34,
        "sequenceSize": 3,
        "sequenceNumber": 2
    }
}
```

## Parameters:

* **originatingAddress** - the source address for MO message
* **destinationAddress** - the destination address for MO message
* **segmentedMessage** - the structure which contains information about the message part received
* **message** - received message part text
* **msgRefNum** - the reference number for all message parts
* **sequenceSize** - the total number of the parts
* **sequenceNumber** - received part number
