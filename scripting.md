# Mesibo Scripting

Mesibo is built by developers for developers. We believe in making our platform open and developer friendly to help you realize your next big idea. In this step, We present to you Mesibo Scripting - An easy to use interface that allows you to use the core platform of Mesibo with the wildly popular Javscript.

Mesibo Scripting offers you variety of functionality that help you interface with the core features of Mesibo over an easy to use Javascript interface.

You can write custom logic in Javascript and let Mesibo Scripting take care of converting that logic into high performance native code. This creates unlimited creative possibilities for building with Mesibo. You can build chatbots, filters, translators, implement socket and database logic all from the comfort and ease of Javascript. 

Mesibo scripting enables you to achieve a tighter integration with your application and greater control over the core platform of Mesibo.

The scripting interface is provided through the Mesibo Cloud console and you need not configure or install anything additional to use it. Just login to your application console , load your script and get going! 

You can also use the scripting module on your own premise/servers if you are [hosting Mesibo](https://mesibo.com/documentation/on-premise/). You can load the scripting module and configure it to run your script.

## How to use Mesibo Scripting
You can specify your customised logic for each event such as when you receive a message, when a user logs in,etc and also use core utility functions provided by mesibo to perform different actions like sending a message, making an HTTP request, connecting to a socket, writing to a database, etc.

From Mesibo Console , you can configure to run a custom script for each user,etc. 

With Mesibo Scripting you can specify your customized logic for each event such as when a user  sends or recieves a message,  when auser logs in,etc and also use core utility functions provided by mesibo to perform different actions like sending a message, makingan HTTP request, connecting to a socket, write to a database, etc. You can build chatbots, filter messages, modify or translate messages and much more to open up unlimited creative possibilities all from the comfort and ease of Javascript.

You can configure a scripts that will be triggered when a user sends data or receives  data. You can also configure a default app script that runs for all events at the app level.
If you are using Mesibo On-Premise you can use the Scripting Module and configure the same.The module interface is provided in native C/C++ platform which ensures raw performance and stability.

## How Mesibo Scripting Works
The script you configure is executed at runtime through the Mesibo Native Interface. This is done by using a Javascript Engine which compiles Javscript code into Native C/C++ code and then evaluating that script on each call.
To do this, Mesibo uses V8 - Google’s open source high-performance JavaScript and WebAssembly engine, written in C++.

## Pricing of the Scripting Platform

Mesibo offers a Pay-as-you-GO pricing model. If you are using Mesibo Scripting on the cloud, you will be charged for running your script on a per-second basis. ie; If your script is active for 10 seconds, then your charge willbe $XX/second * 10 seconds = $YY. 

However, if you are using Mesibo Scripting on your own server by loading the [scripting module]() there are no charges whatsoever.

Please not that all other charges for using Mesibo APIs and services are independent and remain the same.
For more details refer [Mesibo Pricing](https://mesibo.com/pricing/) 


## Examples for using Mesibo Scripting

Here is a glimpse of what you can do with Mesibo Scripting. This code snippet sends a custom reply to any message recieved. 
## Sending an automatic response 

```javascript
mesibo.onmessage = function(message){
	//On receiving a message we send an automated reply to the sender 

	//Create a new Message object
	var replyMessage = new Message();

	//Custom response text/data	
	replyMessage.data = "This is an automated response";

	//Send Message!	
	replyMessage.send();
}
```

The further sections of this document will explain the usage of using various classes you can use in your script,their properties and methods in detail.

- [Mesibo]()
- [Messaging]()
- [Http]()
- [Socket]()

# Mesibo  
The core class `Mesibo` defines a set of callbacks and utilities that you can use to send messages, get message flags, receive messages, etc.  

# Constructor
The class `Mesibo` is not instantiable. A single instance of the class `Mesibo`, named `mesibo` exists in global context whose properties can be initialized. Refer [Usage Notes]() for more details.

# Properties

## `Mesibo.onmessage` <sub>mandatory</sub>  
An event listener to be called when message is receieved. It is mandatory to initialize this event handler.
MUST return Message.PASS, Message.FAIL, Message.CONSUMED, Message.READ, Message.DELIVERED etc, or the message string. 

### Syntax

```javscript
mesibo.onmessage = callback;
```
### Values
- callback is the function to be executed when a message is received. The parameter to this callback function is an object of type [`Message`]()

### Example
```javascript
mesibo.onmessage = function(m){
	var messageText = m.message; 
	print("Got a message from"  + message.peer + " id: " + message.id + " msg: " + messageText);
	return Mesibo.CONSUMED;
}
```

## `Mesibo.onmessagestatus` <sub>optional</sub>  
An event listener to be called when status of the message is recieved. Note that the status for a message will be received only when you set the corresponding flag in the message parameters while sending the message. Initialization of this handler is optional. 

### Syntax

```javascript
mesibo.onmessagestatus = callback;
```
### Values
- callback is the function to be executed when status of a sent message is received. The parameter to this callback function is an object of type [`Message`]()

### Example

```javascript
mesibo.onmessagestatus = function(m){
	print("Message Status : from "  + m.from+ " status: " 
			+ m.status + " id: " + m.id);
}
```

## `Mesibo.onlogin` <sub>optional</sub>  
An event listener to be called when a user logs in or out of your application. Initialization of this handler is optional.

### Syntax

```
mesibo.onlogin = callback;
```
### Values
- callback is the function to be executed when a user logs in or logs out. 

### Example

```javascript
mesibo.onlogin = function(u){
	print("User: "  + u.address + " online status: " + u.online);
}
```

## `Mesibo.onexception` <sub>optional</sub>  
An event listener to be called when an exception occurs 

### Syntax

```
mesibo.onexception = callback;
```
### Values
- callback is the function to be executed to report an exception 

### Example

```javascript
mesibo.onexception = function(e){
	print(e);
}
```

## `Mesibo.OK`  
Indicates Sucessful operation

## `Mesibo.FAIL`  
Indicates Failed Operation

# Global Utility functions 

## `random32()`  
Returns a 32-bit psuedo-random number. 

### Syntax

```javascript
random32()
```
### `Parameters`
None.

### `Return value`
`unsigned 32-bit` integer 

## `random64()`  
Returns a 64-bit psuedo-random number. 

### Syntax

```javascript
random64()
```
### `Parameters`
None.

### `Return value`
`unsigned 64-bit` integer 

## `hash64()`  
Returns a hash of the input. 

### Syntax

```javascript
hash64()
```
### `Parameters`
Any valid object

### `Return value`
A 64 bit hash value 

## `print()`  
Utility to print to console window.
Prints given comma seperated arguments, to console seperated by space.

### Syntax

```
print(string_1, string_2, ... , string_N)
```

### `Parameters`
Comma seperated strings

### `Return value`
`undefined`

### Example

```javascript
print("Hello", "Mesibo");
//Logs 'Hello Mesibo' to console window
```

### Global Session Properties
Session properties exist as a single instance at the global level. Please note that any changes made to the session properties will affect all references to the session object. The following session properties are accessible from all other classes and all of them refer to the singular session instance.

## Mesibo.session_id <sub>read-only</sub>
Session value generted by mesibo. This number describes a session and stays constant throughout the lifetime of the script.
If this value is null, it is a bad session.

## Mesibo.session
Session Object. Properties of this object can be modified to reflect at global level.


The poperties above are accessible from all class objects.
Example, `Mesibo.session`, `Message.session`, `Http.session`, `Socket.session`, `Dialogflow.session`, etc.

# Usage notes

## Instantiation restriction
The class `Mesibo` is not instantiable. 

ie; The following operation is invalid  

```javscript
var m = new Mesibo()
```

Only a single global instance of `Mesibo` class , defined as `mesibo` exists throughout the lifetime of your script. 

## Global Initialization  
It is *necessary* to initialize the event handlers for the global `mesibo` object before you use any other class or function in your script. The handler `mesibo.onmessage` needs to be initialized compulsorily in your script. `mesibo.onlogin` and `mesibo.onmessagestatus` are optional handlers that can be defined if required.

