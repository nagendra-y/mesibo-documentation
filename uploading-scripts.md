## Scripts and Chatbots

## Add scripts to create chatbots, filter messages, modify them, etc.

With Mesibo Scripting you can specify your customized logic for each event such as when a user  sends or recieves a message,  when a user logs in,etc and also use core utility functions provided by mesibo to perform different actions like sending a message, making an HTTP request, connecting to a socket, write to a database, etc. You can build chatbots, filter messages, modify or translate messages and much more to open up unlimited creative possibilities all from the comfort and ease of Javascript.

You can upload and manage all your scripts from your mesibo console.

Follow the steps below to manage scripting for your app.

1. Click on the section `Scripts & Chatbots`

2. Click on `Upload Script` button.

3. Click on `Choose File` button to select and upload a script. Please ensure you are selecting a valid `.js` file and the file sizeis less than 1 MB.

4. Enter a `Description` for the script.

After successfull upload, your script will be displayed with a `Script ID` and `Description`. 

There are three levels to trigger the execution for your scripts:
1. *APP* Specify script at application level. Script will be executed as per your logic for all messages sent and recieved by the users of your application.To execute the script at the default app level, click on the checkbox `Enable Default App Script`
2. *ON RECV* Specify script at the user level. Script will be executed when a message is send to the user.To specify users that link with your script, click on the `*` settings icon and click on the button `Add Script User`. Enter UID(Number) or User Address (Name or any identifier). Select process recieved messages.
3. *ON SENT* Specify script at the user level. Script will be executed when messsage is sent from the user.To specify users that link with your script, click on the `*` settings icon and click on the button `Add Script User`. Enter UID(Number) or User Address (Name or any identifier). Select process sent messages.

On sucessfully adding and specifying your script, the script users will be displayed for that script along with the checkbox selected that shows whether it has been chosen to execute the script when message is received, sent or both.








