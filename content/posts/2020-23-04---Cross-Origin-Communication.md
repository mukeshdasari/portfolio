---
title: Cross Origin Communication - Done Right!
date: "2020-04-23T11:20:32.169Z"
template: "post"
draft: false
slug: "cross-origin-communication"
category: "Web Development"
tags:
    - "JavaScript"
    - "WebDevelopment"
    - "PostMessage"
description: "In web development many times there comes a need to pass the data from one web application to another application. Being in different domains this becomes very challenging. So JavaScript has inbuilt events which can be used to share the data between cross domain web applications."
---

## What is Cross Origin Communication?

Suppose you have two web applications, App1 and App2 with respective origins as www.domain1.com and www.domain2.com. Now we need to send JSON object from App1 to App2. Being in two different domains sharing the data between them is no cup of tea. But using addEventListner and postMessage methods of JavaScript we can pass and get the data. The data sharing between these two different domains is known as Cross Origin Communication.

![Communication](/media/communication-1015376_1920.jpg)

## JavaScript addEventListener and postMessage

The `addEventListener` method will create an Event on the respective window to listen for a particular event to occur. To pass the data we will need to listen for 'message' event to occur on that window to receive it. The basic JavaScript syntax to create event is as follows.

```
window.addEventListener('message',function(event){
}, <useCapture>)
```

The message event will promise the event object which has three properties.

-   **origin** - The origin of the window that sent the message at the time `postMessage` was called.
-   **data** - The data passed from the origin window.
-   **source** - A reference to the window object that sent the data.

When in an application both parent and child elements have event listeners set on them then there are two different ways to define the order or phase in which the event is handled. When the order is from parent to child, it is called **Captured Down**. And when order is from child to parent, its called **Bubbles Up**. So in the Capture down phase, the event will get to that particular element and then to child elements which is a top-down element approach. On other hand in Bubbles up which is default phase, the event will get to children elements first and then to that particular element so it is a down-top element approach.

The **useCapture** in a syntax is a boolean value 'true' for Capture down phase and 'false' for Bubbles up phase.

To send the data we have to use the `postMessage` method of which the syntax is as below.

`targetWindow.postMessage(<message>, <target-origin>)`

-   **targetWindow** is the reference of the window to which the data has to be sent.
-   **message** is the actual stringified data which has to be sent.
-   **target-origin** specifies the URL which is to be of targetWindow at a time of sending the data. And if we need to send the data to all target-origin URLs then we need pass '\*' as a value.

## Examples

### Example 1 - Pop Window

-   **index1.html**

```
<html>
    <body>
        <h1>Page Index1</h1>
        <h2 id="myHeader"></h2>
        <script>
            let popWindow = window.open("./index2.html", "myPopWindow", "width=400, height=600");
            window.addEventListener("message", function (event) {
                document.getElementById("myHeader").innerHTML = event.data;
                popWindow.postMessage("Hello from index1.html", "*");
            }, false);
        </script>
    </body>
</html>
```

-   **index2.html**

```
<html>
    <body>
        <h1>Page Index2</h1>
        <h2 id="myHeader"></h2>
        <script>
            window.opener.postMessage("Hello from index2.html", "*");
            window.addEventListener("message", function (event) {
                document.getElementById("myHeader").innerHTML = event.data;
            }, false);
        </script>
    </body>
</html>

```

### Example 2 - Iframe

-   **index1.html**

```
<html>
    <body>
        <h1>Page Index1</h1>
        <h2 id="myHeader"></h2>
        <iframe id="myIframe" src="./index2.html"  width="400" height="600" style="border: 1px solid black;"></iframe>
        <script>
            let myIframeWindow = document.getElementById("myIframe").contentWindow;
            window.addEventListener("message", function (event){
                document.getElementById("myHeader").innerHTML = event.data;
                myIframeWindow.postMessage("Hello from index1.html", "*");
            }, false);
        </script>
    </body>
</html>

```

-   **index2.html**

```
<html>
    <body>
        <h1>Page Index2</h1>
        <h2 id="myHeader"></h2>
        <script>
            window.parent.postMessage("Hello from index2.html", "*");
            window.addEventListener("message", function (event) {
                document.getElementById("myHeader").innerHTML = event.data;
            }, false);
        </script>
    </body>
</html>

```

## Conclusion

When the data has to be sent from an Iframe then `window.parent.postMessage(<message>, <target-origin>)` is used as window.parent is the reference of the parent window. And when the data has to be sent from an Pop Window then `window.opener.postMessage(<message>,<target-origin>)` is used as in this case window.opener is the reference of the parent window. In this way the data has been passed to cross origin applications.
