1. ### Event Loop and Async js

    The event loop is a process that continuously monitors both the call stack and the event queue and checks whether or not the call stack is empty. If the call stack is empty and there are pending events in the event queue, the event loop dequeues the event from the event queue and pushes it to the call stack. The call stack executes the event, and any additional events generated during the execution are added to the end of the event queue.

    ```javascript
    const one   = () => console.log("First");
    const two   = () => setTimeout(()=>console.log("Second"),500);
    const three = () => console.log("Third");

    two();
    one();
    three();
    ```
    ```excalidraw

eventloop.excalidraw.png

```