## Mesibo Dialogflow Chatbot
With Mesibo scripting you can easily interface with chatbot and NLP engines like Dialogflow, IBM watson, Microsoft Azure Bot Services, etc. You can build powerful chatbots to craft novel messaging experiences all with the ease of Javascript with Mesibo Scripting.

Here, we show you an example of using Dialogflow to build a powerful chatbot that can do basic small talk.

### Prerequisites
- We will not get into the details of building the Dialogflow agent from scratch. Please refer to the [Dialogflow Docs](https://cloud.google.com/dialogflow/docs/quick/api) for learning the basics of Dialogflow and building your chat agents.
- [Building a chatbot with Mesibo](https://mesibo.com/documentation/on-premise/loadable-modules/#code-references-and-examples) fro a quick review on building a simple chatbot with Mesibo Modules

## Building an FAQ chatbot

### 1. Create a Dialogflow agent
Go to Dialogflow Console and create an agent with the project name `mesibo-dialoflow`. Refer [Creating an Agent](https://cloud.google.com/dialogflow/docs/quick/api#create-an-agent)

### 2. Import the Mesibo Chatbot Sample 

To import the chatbot sample, follow these steps:

Download the [MesiboChatbotSample.zip]() file
1. Go to the Dialogflow Console
2. Select your agent
3. Click the settings settings button next to the agent name
4. Select the Export and Import tab
5. Select Import From Zip and import the zip file that you downloaded

### 3. Getting hands-on with scripting 
Each message from the user contains is a query. Do deliver an appropriate response, we need to find the [`intent`](https://cloud.google.com/dialogflow/docs/quick/api#detect_intent) behind that query. Based on the training data, the query is analysed to match a set of intents. We select the appropriate response to the intent that matched with the highest `detectionConfidence` and send the response linked with that intent. The intent with the highest `detectionConfidence` is matched and the response is stored in `responseText`

### Sending a request to Dialogflow
You need to send the following information to Dialogflow to get a valid response.

- `Project ID`: Use the project ID for the project you created in the setup steps. Here, the project  name is `mesibo-dialogflow`
- `Session ID`: For the purpose of testing an agent, you can use anything. Here, we pass the `message-id`

```javascript
//POST https://dialogflow.googleapis.com/v2/projects/project-id/agent/sessions/session-id:detectIntent
const gDialogflowUrl = "https://dialogflow.googleapis.com/v2/projects/mesibo-dialogflow/agent/sessions/"
const gDialogflowToken = <Access Token>
	const gMesiboChatbotUser = <Mesibo Chatbot User ID>

	initialize();

function initialize(){
	mesibo.onmessage = Mesibo_onMessage;
	mesibo.onmessagestatus = Mesibo_onMessageStatus;
}

function Mesibo_onChatbotResponse(h) {
	var rp = JSON.parse(h.responseJSON);
	var fulfillment = rp.queryResult.fulfillmentText;

	var query = h.query;
	var chatbot_response = query;
	chatbotResponse.from = query.to;
	chatbotResponse.to = query.from;
	chatbotResponse.message = fulfillment;
	chatbotResponse.refid = query.id;
	chatbotResponse.id = parseInt(Math.floor(2147483647*Math.random()));

	chatbotResponse.send();

	return mesibo.RESULT_OK;
}

function Mesibo_onMessage(m) {
	//Filter messages which are addressed to the chatbot
	if(m.to == gMesiboChatbotUser){
		var dHttp = new Http();
		//POST https://dialogflow.googleapis.com/v2/projects/project-id/agent/sessions/session-id:detectIntent
		dHttp.url =  gDialogFlowUrl +m.id+ ":detectIntent";
		var request_body = {
			"queryInput": {
				"text": {
					"text": m.message",
					"languageCode" : "en"
				}
			}
		};
		dHttp.post = JSON.stringify(request_body);
		dHttp.ondata = Mesibo_onChatbotResponse;
		dHttp.query = m;
		dHttp.extraHeaders = "Authorization: Bearer"+ gDialogflowToken; 
		dHttp.contentType = 'application/json';
		dHttp.send();
	}
	return mesibo.RESULT_OK;
}
```

For sending the request to the dialogflow chatbot we send the message-id to identify the [session](https://cloud.google.com/dialogflow/docs/quick/api#sessions) and in the response that we send back to the user , the `refid` will have the message-id of the query message. This way the client who sent the query can know which message query is the given response linked to.

