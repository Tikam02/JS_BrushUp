ref :

https://medium.com/@gaurav.pandvia/understanding-javascript-function-executions-tasks-event-loop-call-stack-more-part-1-5683dea1f5ec 

https://www.freecodecamp.org/news/understanding-the-javascript-call-stack-861e41ae61d4

https://dev.to/lydiahallie/javascript-visualized-event-loop-3dif

https://blog.carbonfive.com/the-javascript-event-loop-explained/

https://flaviocopes.com/javascript-event-loop/



Javascript is a single threaded single concurrent language, meaning it can handle one task at a time or a piece of code at a time. It has a single **call stack** which along with other parts like heap, queue constitutes the Javascript Concurrency Model (implemented inside of V8).


![](https://miro.medium.com/max/598/1*ZSFHnq9iMHIApVLcgwczPQ.png)



**1.Call Stack :-** It’s a data structure which records the function calls, basically where in the program we are. If we call a function to execute , we push something on to the stack, and when we return from a function, we pop off the top of the stack.

Sometimes, we get into an infinite loop as we call a function multiple times recursively and as for Chrome browser, there is a limit on the size of the stack which is 16,000 frames , more than that it will just kill things for you and throw **Max Stack Error Reached (image below).**


**2.Heap** :- Objects are allocated in a heap i.e mostly unstructured region of memory. All the memory allocation to variables and objects happens here.


**3.Queue** :- A JavaScript runtime contains a message queue, which is a list of messages to be processed and the associated callback functions to execute. When the stack has enough capacity, a message is taken out of the queue and processed which consists of calling the associated function (and thus creating an initial stack frame). The message processing ends when the stack becomes empty again. In basic words , these messages are queued in response to external async events(such as a mouse being clicked or receiving the response to an HTTP request), given a callback function has been provided. If, for example a user were to click a button and no callback function was provided — no message would have been enqueued.

![](https://miro.medium.com/max/1400/1*-MMBHKy_ZxCrouecRqvsBg.png)


The call stack is primarily used for function invocation (call). Since the call stack is single, function(s) execution, is done, one at a time, from top to bottom. It means the call stack is synchronous.

What is the call stack?

At the most basic level, a call stack is a data structure that uses the Last In, First Out (LIFO) principle to temporarily store and manage function invocation (call).

**Temporarily store**: When a function is invoked (called), the function, its parameters, and variables are pushed into the call stack to form a stack frame. This stack frame is a memory location in the stack. The memory is cleared when the function returns as it is pop out of the stack.


![](https://blog.carbonfive.com/wp-content/uploads/2013/10/event-loop.png)



```js

const foo = () => console.log("First");
const bar = () => setTimeout(() => console.log("Second"), 500);
const baz = () => console.log("Third");

bar();
foo();
baz();

```


![](https://res.cloudinary.com/practicaldev/image/fetch/s--BLtCLQcd--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_880/https://devtolydiahallie.s3-us-west-1.amazonaws.com/gif14.1.gif)


**The loop gives priority to the call stack, and it first processes everything it finds in the call stack, and once there’s nothing in there, it goes to pick up things in the message queue.**