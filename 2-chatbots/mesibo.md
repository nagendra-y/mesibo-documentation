---
description: Mesibo Class 
keywords: chatbot, script, scripting
title: Mesibo 
---

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

## Mesibo.session_id <sub>read-only</sub>
Session value generted by mesibo. This number describes a session and stays constant throughout the lifetime of the script.
If this value is null, it is a bad session.

## Mesibo.session
Session Object. Properties of this object can be modified to reflect at global level.

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

