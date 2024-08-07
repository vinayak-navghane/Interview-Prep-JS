1. ### Event Loop and Async js

    Javascript is single threaded language but we do see asynchronous non-blocking behaviour in javascript. This behaviour is possible because of Event Loop
    
    The event loop is a process that continuously monitors both the call stack and the event queue and checks whether or not the call stack is empty. If the call stack is empty and there are pending events in the event queue, the event loop dequeues the event from the event queue and pushes it to the call stack. The call stack executes the event, and any additional events generated during the execution are added to the end of the event queue.

    ```javascript
    const one   = () => console.log("First");
    const two   = () => setTimeout(()=>console.log("Second"),500);
    const three = () => console.log("Third");

    two();
    one();
    three();
    ```
    ![Event Loop](eventLoop.excalidraw.png)

    Output : 
            First
            Third
            Second

    Explanation : 
    1. two() get called first hence it is moved to call stack and then to Browser API's.
       then it get executed in Browser API's and then moved to macro task queue.

    2. while two is in macro task queue, one() gets called, being moved to call stack and prints "First".

    3. three() get called , being moved to call stack and prints "Third".         

    4. Event loop first checks micro tasks queue, which is empty then checks macro task queue and moves two to call stack for execution and prints "Second".