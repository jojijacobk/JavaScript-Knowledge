# About Javascript

<img src="https://github.com/jojijacobk/_draw.io/raw/master/About%20Javascript.png" width="1000"/> <br/>

Javascript is a general purpose <span class="underline">scripting
language</span>, which is an implementation of <span
class="underline">ECMAScript specification</span> based on <span
class="underline">ECMA 262 standard</span>.

-   **Ecma International** is an organization that creates standards for
    technologies. They have created several standards for various
    technologies, whereas the standard code named as **ECMA 262**
    defines a <span class="underline">scripting language specification
    called **ECMAScript**</span>.
-   **ECMA 262** is a standard, for example, similar to QWERTY layout
    standard. Every keyboard manufacturers can make their own brand of
    keyboard compliant to QWERTY layout standard. Similarly, the
    specification provided by ECMA 262 standard known
    as ECMAScript provides the rules, standards and guidelines on making
    a scripting language to be considered as ECMAScript compliant.
    ES2015, ES2016 etc are different versions of ECMA 262 standard.
-   A **scripting language** is a programming language designed to act
    specifically on an external entity.  For example Javascript is a
    scripting language targeting at external entities such as browser,
    node.js server etc.
-   Reading _ECMAScript specification_
    helps to understand how to make a scripting language like
    Javascript.
-   Reading _Javascript documentation_
    helps to understand how to use this script language to get things
    done.
-   A **Javascript engine** is a program that understands and executes
    javascript. Eg: _V8 engine for Chrome_,
    _Chakra for Edge_, _SpiderMonkey for FIrefox_
    -   **V8 engine** for Javascript is very fast because the Javascript
        code is directly translated to machine code by V8 by using a
        JIT. There is no intermediate code (interpreted code), hence
        making the execution very fast.
-   The same javascript engine can work on different runtime
    environments. For eg: V8 engine works for Chrome as well as Node.js
    server
-   A **Javascript runtime** is an environment which provides a host of
    objects for javascript to operate on, and is executed by javascript
    engine. So, Browser is a javascript runtime which provides a host of
    objects such as window, document, HTML elements etc which is
    operated on by javascript, and is executed by a javascript engine
    inside this javascript runtime environment. It is the runtime
    environment (browser) that provides the web apis to work on these
    host of objects.

| Language   | Runtime | Engine which executes code |
|------------|---------|----------------------------|
| Java       | JRE     | JVM                        |
| Javascript | Node    | V8                         |
| Javascript | Browser | V8                         |

## Javascript Engines


|Engines|Sponsors|Built using|
|-------|---------|----------|
|V8|Maintained by Google as open source, used by Chrome & Node.Js|C++|
|SpiderMonkey|Started by Netscape, maintained today by Firefox||
|Rhino|Maintained by Mozilla Foundation as open source|Java|
|JavascriptCore (aka Nitro)|Maintained by Apple for Safari|
|Chakra|IE, Edge||
|JerryScript|IoT||
|Nashorn|open source as part of OpenJDK by Oracle||
|KJS|for KDE, used by Konqueror||

# Event Loop

- **Javascript engine** is not working alone. It resides inside a _hosting environment_. Javascript engine doesn't have an innate sense of time. It is the hosting environment that schedules code snippets to run by adding them to **event loop**. Javascript engine simply executes whatever snippets of code is given to it. If the file contains only a programs which are meant to be run sequentially, they are executed in a single stretch. But, if the program is met with asynchronous functions, Javascript engine executes those functions and ask host environment to put callback into the event loop queue once response data needed by the callback function is ready.
  
  **Exmamples of working of event loop:**
    **Eg 1**: When a `setTimeout` function is processed, Javascript engine executes that code, and handover callback function to the hosting environment which keeps it aside for the configured period of timeout, and then pushes the callback of setTimeout function into the event loop.

    **Eg 2**: When an Ajax function is run, Javascript engine would execute the function and realize that it is demanding a callback when there is data. So, it asks the hosting environment to invoke the callback when there is response coming back from the Ajax request. Once there is data, hosting environment would put that callback function into event loop - which is executed by Javascript engine. So, the asynchronous nature of Javascript was achieved with the help of hosting environment until ES6. Then, **Promise** arrived, for which there is a nuanced behaviour with the introduction of **Job queue**.

- You can assume the way Javascript engine works in the event loop is similar to the way human brain works. Human's aren't capable fo multi-tasking. All what a human brain does at the forefront of minds is to simply do context-switching.

# Job Queue
- Each iteration of *event loop* is called a *tick*, where the next item to execute as present in top of the even loop queue is pulled into execution. When you have a callback function ready for execution (from ajax or setTimeout) it is put into the end of this event loop queue. But, if you use **ES6 Promise, it helps to put callback functions into the end of current tick itself**. You can thus put more items into this queue forming a special *Job queue* which is guaranteed to execute after current tick and before picking up next item in the event loop. But, if you continuously add items into the Job queue then you end up with same situation like an infinite loop preventing next item in event loop to be executed.

# Asynchronous execution

- While you log data to console for debugging purpose, it may occur that data logged via `console.log(data)` is not showing correct value as expected. This is because, as it is an I/O bound operation, browser tends to run it in the background asynchronously, hence logging actually works at a later point of time, and by then the logged values might have already been changed. Better alternatives are :
  - use breakpoints 
  - save snapshots of objects by using `JSON.stringify(data)`

- Javascript doesn't have multi-threading concept. Hence, the execution of a code snippet follows the rule of **run to completion** except for ES6 generators.
  But, in Javascript also there is **non deterministic ordering of functions**.

__For eg__: When there are a couple of ajax calls waiting to operate on a shared data, then both competes to reach first in performing callback function. This is a special condition called *race condition*.

## Callback

- Callbacks are the simplest unit of asynchronous implementation. But, it is not the most elegant form because of the following concerns:

### Drawbacks of _callback pattern_:
  - Callbacks are not easy to contemplate by human brain. They doesn't let human brain to think in sequential manner. Certainly when the levels of callbacks go deeper in a large program with several of such repetitions, it is not going to be anywhere near comprehensible.
  - Another drawback is the trust issue because of _inversion of control_. A callback function may be invoked by a 3rd party code. You don't have any control over it. They may fail to call your code, or call multiple times, or call too early, or call lately, or miss some parameters necessary for the call.
- These disadvantages calls for the need for a better asynchronous orchestration - that's **ES6 Promise**.

## Promise

Instead of leaving the life of a callback invocation into the hands of asynchronous API (eg: ajax 3rd party API), it is quite anticipated to have a mechanism to understand when the asynchronous API's work is finished. This is what a Promise offers us. Promise let us to sequentially think and work based on the _future value_ now itself.

## Promise examples 
```Javascript
/* eslint-disable prefer-promise-reject-errors */

// 1. 'simple resolve --------------------------------------------------------';
const p1 = new Promise((resolve, reject) => {
  resolve('p1 resolved');
});
p1.then((resolvedValue, rejectedValue) => {
  if (resolvedValue) console.log(resolvedValue);
  if (rejectedValue) console.log(rejectedValue);
});

// 'simple reject ---------------------------------------------------------';
const p2 = new Promise((resolve, reject) => {
  reject('p2 rejected');
});
p2.then(
  resolvedValue => {
    console.log(resolvedValue);
  },
  rejectedValue => {
    console.log(rejectedValue);
  }
);
// 'simple reject, catch it ---------------------------------------------------------';
const p2x = new Promise((resolve, reject) => {
  reject('p2x rejected');
});
p2x.catch(rejectedValue => {
  console.log(rejectedValue);
});

// 'resolve, and finally ---------------------------------------------------';
const p3 = new Promise((resolve, reject) => {
  resolve('p3 resolved');
});
p3.then((resolvedValue, rejectedValue) => {
  if (resolvedValue) console.log(resolvedValue);
  if (rejectedValue) console.log(rejectedValue);
}).finally(() => {
  console.log('Finally of p1');
});

// 'wait for ALL promises, all are resolved  --------------------------------'
Promise.all([p1, p3]).then(
  resolvedValue => {
    console.log(resolvedValue);
  },
  rejectedValue => {
    console.log(rejectedValue);
  }
);

// 'wait for ALL promises, if any is rejected, then the WHOLE is rejected ----------------------------------'
Promise.all([p1, p2]).then(
  resolvedValue => {
    console.log(resolvedValue);
  },
  rejectedValue => {
    console.log(rejectedValue);
  }
);
// 'race with ALL promises, only first fulfillment or rejection (whichever comes first) is considered ---------------------------'
Promise.race([p1, p2]).then(
  resolvedValue => {
    console.log(resolvedValue);
  },
  rejectedValue => {
    console.log(rejectedValue);
  }
);
```
# Performance
Javascript doesn't have multi-threading feature, but for performance sake if there was a possibility to run a piece of program in parallell which doesn't need to share resource with main program, that would be pretty useful. HTML5 realized this opportunity and introduced _Web Workers_. 

## Web Workers
A worker thread is a feature provided by hosting environment (browser), its not part of Javascript because there is no multi-threading in Javascript. 

### Dedicated worker
The worker threads are like a separate browser instance with separate Javascript engine and works on a separate process as compared to the main program. You can create a dedicated worker from main program or from another worker as follows:

```Javascript
const w1 = new Workder('path.tofile.js'); // also accepts binary blob of JS file instead of file itself.
w1.addEventListener('message',(data)=>{
    console.log(data);
})
w1.postMessage(data);
```
You can offload activities such as loading several scripts, other high network traffic, image processing, complex CPU intensive math calculation etc in the worker thread. And, once data is processed it can be send back to main program through message events. 

#### Data transfer
Data transfer through message events simply works by copying information from source to destination (main -> worker or worker-> main) using **structured cloning algorithm**. This is memory intensive because your data has to be copied, thus doubling size in memory. New age workers are efficient to simply change ownership of data instead of copying from one location to another. Hence, the only condition for that data is that it should implement _Transferable_ interface.

If an app/page using worker is opened in multiple tabs of browser, it causes duplication of workers, which is performance bound. This can be fixed using _Shared Workers_.

### Shared worker
A shared worker can operate with several source/target programs in shared state using a single worker. To identify browser tab/instance of page is facilitated using _ports_. When you create a worker from a tab to the Javascript file/blob, Shared worker is instantiated and connects to that tab via a port. Similarly, any other tabs will connect with different ports to the same shared worker.
