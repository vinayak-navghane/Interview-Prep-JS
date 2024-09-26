1. ### What is Event Loop and Async javascript

    Javascript is single threaded language but we do see asynchronous non-blocking behaviour in javascript. This behaviour is possible because of Event Loop.

    When an asynchronous task such as HTTP request or a DOM event is initiated, it is handed off to browser API's. Once these tasks are completed, their callbacks are placed into either microtask(priority) queue or the macrotask queue, depending upon the nature of the event.
    
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


2. ### What is Hoisting

    In JavaScript, before executing any code, the JavaScript engine performs a memory preparation phase known as hoisting. During this phase, the engine allocates memory for variables and functions:

     1.Function declarations are fully hoisted, meaning they can be invoked anywhere within their scope, even before their actual line of declaration.

     2.Variables declared with var are hoisted and initialized with undefined. This means you can access var variables before their declaration, but their value will be undefined.

     3.Variables declared with let and const are also hoisted but remain uninitialized. Accessing them before their declaration in the code results in a ReferenceError.

    This period between the start of the block and the actual declaration of a let or const variable is called the Temporal Dead Zone (TDZ). The TDZ exists from the start of the block until the line where the variable is declared and initialized.
    