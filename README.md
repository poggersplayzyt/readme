# readme

from 3dsboy08:

```js
const connectionUrl = "ws://localhost:24892/execute";
const spamData = "print'hi'";

function spamWS(){
    const socket = new WebSocket(connectionUrl);
    var shouldContinue = true;

    socket.addEventListener('open', e => {
        console.log("[Info] WS-OPENED");
        
        const timer = setInterval(() => {
            if(!shouldContinue) return clearTimeout(timer);
            socket.send(spamData);
        }, 50);
    });
    socket.addEventListener('close', e => {
        shouldContinue = false;
        setTimeout(() => {
            console.log('[Info] WS-Closed, reconnecting (1000ms)');
            spamWS();
        }, 1000);
    });
    socket.addEventListener('message', e => {
        console.log("[WS-MESSAGE]", e.data);
    })
}

spamWS()
```
