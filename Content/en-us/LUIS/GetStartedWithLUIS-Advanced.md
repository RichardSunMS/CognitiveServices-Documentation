<!-- 
NavPath: LUIS API
LinkLabel: Get Started With LUIS-Advanced
Url: LUIS-api/documentation/GetStartedWithLUIS-Advanced
Weight: 97 
-->

#Get Started with LUIS: Advanced Features

######Adding advanced features to your basic LUIS application

###Action Binding

 There are times when you may want to link an intent to an action. You can also specify requirements for this action to be triggered. These requirements are known as parameters. LUIS supports only one action per intent. Each action can include a group of parameters derived from entities. The parameter can be optional or required, LUIS assumes that an action is triggered only when all the required parameters are fulfilled. 

###Defining an Action

1. In the LUIS Application Editor work space on the left-hand panel, click an existing intent, for example "BookFlight", or create a new one.
2. In the **Add a new intent** dialog box which opens, click **Add Action**.
3. Let us assume this action requires three parameters, "FromLocation", "ToLocation", and "Date".
4. Click **Add Parameter**. Type the name of the parameter, for example "FromLocation", and specify its type from the entities in the **Type** drop-down menu. In this case "Location::FromLocation" is the entity. (For hereditary entities, see [Get started with LUIS: The Basics](GetStartedWithLUIS-Basics.md).)
5. Click **Add Parameter** again to add the next parameter, for example "ToLocation" with "Location::ToLocation" being the entity.
6. Add a third parameter "Date" with "datetime" being the entity.
7. Check the **Required** check box next to the name of the parameter that is required for the action to be triggered. (If the action is optional, leave the check box unchecked.)

![Adding Action Binding](./Images/AddActionBinding.PNG)

**Notes:**
To delete a parameter, click the trashcan next to its field. To delete an action with its parameters, click **Delete Action** from inside the **Add a new intent** dialog box.

###Action Fulfillment (Preview)

This feature enables you to fulfill the actions that were trigged through a set of channels. For example, if you created the "GetWeather" intent and the action has been triggered (all the required parameters were filled), you can use the GetCurrentWeather channel to retrieve the weather for your users to see. 

LUIS is providing a first set of channels and actions, expect to see more soon. For a full list of current channels, see [Channels](Channels.md).

![Action Fulfillment](./Images/AddFulfillment2.PNG)

Follow these steps (see above screenshot): 

1. In the top teal-colored ribbon of the LUIS Application Editor work space, click **Go to Preview**.
2. Find Intents in the left-hand menu panel, then click the intent for which you want to bind an action, in this case “GetWeather”. 
2. In the **Add a new Intent** dialog box, click **Add Action**. This will open the dialog box as shown in above screenshot.
3. Check **Fulfillment** in the **Action Info** sub-section to enable action types.
4. From the Action Type drop-down list, select "GetCurrentWeather".
5. In the Action Parameters sub-section, click **Add Parameter** to add a new line.
6. Check the box if the parameter is required, add parameter name, type, value and a text prompt, which is displayed if the parameter is not provided with the intent. (In above screenshot: “required”, “location”, “location”, “locations”, “Which place?”) 
7. In the **Action Settings** sub-section, map the action to a parameter from the **Append a Parameter** drop-down list, in this case “location”.
8. Click **Save** to complete and exit.

###JSON response

This is an example of the JSON response that is returned when an action is fulfilled. 
```
{
  "query": "paris",
  "topScoringIntent": {
    "intent": "BookFlight",
    "score": 0.924560249,
    "actions": [
      {
        "triggered": false,
        "name": "BookFlight",
        "parameters": [
          {
            "name": "Destination",
            "required": true,
            "value": [
              {
                "entity": "paris",
                "type": "Location::ToLocation"
              }
            ]
          },
          {
            "name": "Source",
            "required": true,
            "value": null
          },
          {
            "name": "Travel Date",
            "required": true,
            "value": null
          }
        ]
      }
    ]
  },
  "entities": [],
  "dialog": {
    "prompt": "From where?",
    "parameterName": "BookFlight::Source",
    "contextId": "2dc6f283-b43d-4312-aee4-1d9c2f0f94dc",
    "status": "Question"
  }
}

```
Notice that the "Destination" required parameter is set to TRUE, which means they are filled in. Thus the action will be triggered as all its required parameter is available.

###Dialog Support (Preview)

LUIS allows you to add conversational interfaces to your applications through a new powerful dialog engine. You can author and execute your dialog in just a few steps. For example, if the user is searching for flights to Paris and typed an utterance without specifying one of the required parameters, "FromLocation", LUIS consequently will send a prompt question "From where?". 

After defining all the parameters needed for action triggering, you now have the ability to add a prompt question, if any of the required parameters is missing. This is where the dialog comes in and here is how you can build and consume this feature. 

###Dialog Authoring

1. Click **Go to Preview** in the top ribbon, and then click "BookFlight" intent in the upper left-hand menu panel. In the **Add a new intent** dialog box, all parameters previously listed in the **Production** mode will be displayed. Note: To return to the **Production** mode, click **Back to Production** in the top ribbon. 
2. Select the **Required** check box next to the name of the parameter that must be present for the action to be triggered. In this way, questions will be prompted when users issue queries that do not include the required parameter. 
3. Specify the parameter value from the phrase list in the **Value** drop-down list.
 Notes: Phrase lists are not used with pre-built entities.
Phrase lists work with parameters the same way they work with utterances, they are considered features that improve the accuracy of parameters in the utterances. 

4. In the **Prompt** text box, type the question to be surfaced when the required parameter is missing. 
5. Use the up and down arrows to define the order in which your application will ask these questions. 
6. Click **Save**. 

![Adding prompts](./Images/AddingPrompts.PNG)

###Dialog Execution

Testing the query "BookFlight". Here is the JSON response snippet from a dialog response: 

```
        "dialog": 
  {
    "prompt": "From where?",
    "parameterName": "Location::FromLocation",
    "contextId": "09629512-7310-4a9d-9411-57e1d7f8022b",
    "status": "Question"
  }
```
Notes: 
A new dialog section appears at the end of the JSON response. Only the top scoring intent is returned in the JSON response.

To continue the dialog, append the answer to the question along with the contextID as request parameter. Example: &q=departure date &contextId= a144a208-2f1f-4faf-877b-8898ec523022 

Here is the JSON repsonse snippet from the following dialog question: 
```
    "dialog":  
 {
    "prompt": "Which date?",
    "parameterName": "Date::datetime",
    "contextId": "2e48c7e0-d343-465f-ab0d-03a7598b655f",
    "status": "Question"
  }
```
###Summary

You have learned to add actions and interactive dialog features to your LUIS application. To publish your application to a bot where the benefits of these advanced features will be showcased, see [Slack / Microsoft Bot Framework Integration](PublishingToABot.md).

