<!-- 
NavPath: LUIS API
LinkLabel: Pre-built Application
Url: LUIS-api/documentation/Pre-builtApplication
Weight: 88 
-->


#Pre-built application v2

In addition to allowing you to build your own applications, LUIS also provides selected models from the Microsoft Cortana personal assistant as a pre-built application. To use it, click on the "Cortana pre-built app" at the top of your list of LUIS applications. 

For example, the utterance "**set up an appointment at 2:00 pm tomorrow for 90 minutes called discuss budget**" returns:
```
    {
	  "q": "set up an appointment at 2:00 pm tomorrow for 90 minutes called discuss budget",
	  "entities": [
		{
		  "resolution": {
			"resolution_type": "builtin.datetime.time",
			"time": "T14:00"
		  },
		  "type": "builtin.calendar.start_time",
		  "entity": "2:00 pm"
		},
		{
		  "resolution": {
			"date": "2015-10-19",
			"resolution_type": "builtin.datetime.date"
		  },
		  "type": "builtin.calendar.start_date",
		  "entity": "tomorrow"
		},
		{
		  "resolution": {
			"duration": "PT90M",
			"resolution_type": "builtin.datetime.duration"
		  },
		  "type": "builtin.calendar.duration",
		  "entity": "90 minutes"
		},
		{
		  "type": "builtin.calendar.title",
		  "entity": "discuss budget"
		}
	  ],
	  "intents": [
		{
		  "intent": "builtin.intent.calendar.create_calendar_entry"
		}
	  ]
	}
  ```  

This is an "as-is" application: the intents and entities in this application cannot be edited or integrated into other LUIS applications. If you’d like your client to have access to both this pre-built LUIS application and your own LUIS application, your client can make 2 separate HTTP calls. 

The pre-built personal assistant application is available in all LUIS application cultures (locales), that is English, French, Italian, Spanish and Chinese. 

Earlier versions

Version 1 of the pre-built application continues to be available, but has been deprecated. For developers continuing to use version 1, the documentation is available [here](https://www.luis.ai/Help/AssistantV1). 
