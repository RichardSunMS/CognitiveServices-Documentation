<!-- 
NavPath: LUIS API
LinkLabel: Channels
Url: LUIS-api/documentation/Channels
Weight: 80 
-->

#Channels

A channel is a collection of related fulfillments. The following list shows the possible fulfillments available. 

If you want to use the channels, you must first add [LUIS Action Binding](GetStartedWithLUIS-Advanced.md) to your [Slack](https://slack.com/signin?redir=%2Foauth%2Fpick%2F39337220033.d12e11480e) environment. 
 

###Definition Channel

######Description

The definition channel returns definitions for given words.

######Actions


   Action Name   |   Action Settings   |   Values   |   Examples|
|------|------|------|-------|
GetDefinition  | Entity*  | --  | What is the definition for apple? What does emotion mean? |

Prebuilt app: You can download a prebuilt app supporting our sample utterances for this action [here](https://www.luis.ai/Content/sampleApps/Build_Define_v1.1.json).

###HTTP Channel

######Description

The HTTP channel is a generic channel to enable bindings to arbitrary REST endpoints. It is the most flexible channel that can be adapted to the needs of your service. It supports both anonymous requests and basic authorization headers. 

######Actions

 Action Name   |   Action Settings   |   Values   |   Examples|
|------|------|------|-------|
JsonRequest    |    Verb*, Url*, Body, Username, Password, Response Template    |   ```{GET, PUT, POST, DELETE}```    |   --   |

######Additional Details

This action sends a request to the URL given as an action setting. Depending on the Verb setting the request can be a GET, POST, PUT, or DELETE request. If a basic authorization header should be added, the Username or Password setting (or both) cannot be empty. 

For POST and PUT, a body for the request can be given in the Body setting. If a value for that setting is given, it has to be in JSON format (the request is sent with content type “application/json”). Also, a response is expected to be in JSON format. Note, that values within single curly brackets will be treated as references to action settings like in any other action setting. Therefore, all brackets in the body have to be escaped by doubling them. For example, imagine a service expects the following JSON body: 
```
{
  "Animals":
  [
    {
      "Animal":"fox",
      "Attribute":"quick brown"
    },
    {
      "Animal":"dog",
      "Attribute":"lazy"
    }
  ]
}
```

Note you should escape the brackets (with an additional “{“) to list the values in the Body setting (see below)
{{
```
"Animals":
  [
    {{
      "Animal":"fox",
      "Attribute":"quick brown"
    }},
    {{
      "Animal":"dog",
      "Attribute":"{builtin.attribute}"
    }}
  ]
}}
```

This way you can still use placeholders for action within the setting, for example, to set the value of a field (see attribute value in example).

If the ResponseTemplate action setting is empty, the response will be the JSON returned from the service. However, using the ResponseTemplate you can construct a natural language response from the fields of the JSON structure using a JPath expression within double curly brackets. Again, anything within single curly brackets will be treated as a reference to an action parameter. For example, imagine your service returns a JSON structure like the one displayed above. Then you can construct a natural language response using the response template like this: 

The ```{{Animals[0].Attribute}} {{Animals[0].Animal}} jumps over the {{Animals[1].Attribute}} {{Animals[1].Animal}}```. 

The expected response would then be: ```The quick brown fox jumps over the lazy dog.```
If not all placeholders can be filled from the JSON, they will be left empty. If the service returns an error status code, this error code will be shown to the user instead. 

###News Channel

######Description

The news channel allows for sending a search query and get back a list of relevant news articles.

######Actions

Action Name   |   Action Settings   |   Values   |   Examples|
|------|------|------|-------|
   GetNews   |   Topic    |  --  |    What are the top news? What are the news in sports? Any news about Microsoft?  

Prebuilt app: You can download a prebuilt app supporting our sample utterances for this action [here](https://www.luis.ai/Content/sampleApps/Build_News_v1.1.json).

######Additional Details

The parameter topic is optional. If no parameter is given, the top news stories are returned. To request news articles by category, specify the category name as parameter. Currently, the following categories are supported: Business, Entertainment, Health, Politics, ScienceAndTechnology, Sports, US, World. If the parameter is given but not one of the support categories, news articles that are relevant to the specified topic are returned. The top 3 related news articles are returned. Each news article contains a title, a short description, and a URL link for the complete news article. At this point in time, the news channel only supports the en-US market. 

###Utility Channel

######Description

The pass-through channel returns text, similar to an echo service.

######Actions

Action Name   |   Action Settings   |   Values   |   Examples|
|------|------|------|-------|
   WriteLine   |   Text     |   --  |   What can I say? What can I do?   |
 
Prebuilt app: You can download a prebuilt app supporting our sample utterances for this action [here](https://www.luis.ai/Content/sampleApps/Build_Help_v1.0.json).

###Stocks Channel

######Description

The stock channel provides stock information. It returns news covering the major financial markets and lists stock tickers for DOW and Nasdaq stock indexes and local stock exchanges. 

######Actions

Action Name   |   Action Settings   |   Values   |   Examples|
|------|------|------|-------|
   GetPrice   |    Symbol*     |   --   |   What is the stock price of MSFT?   |

Prebuilt app: You can download a prebuilt app supporting our sample utterances for this action [here](https://www.luis.ai/Content/sampleApps/Build_Stock_v1.1.json).

###TimeZone Channel

######Description

The time zone channel provides time information from around the World.

######Actions

Action Name   |   Action Settings   |   Values   |   Examples|
|------|------|------|-------|
   GetTime   |   Location*    |   --   |   What time is it in New York? What time is it in California?   |

Prebuilt app: You can download a prebuilt app supporting our sample utterances for this action [here](https://www.luis.ai/Content/sampleApps/Build_Timezone_v1.1.json).

######Additional Details

The time zone channel returns the local time of the given location. A location can be a city, a state, or a country. The answer provides the name of the location, the current date and time at the specified location, and the current UTC offset (daylight saving time is considered). If the boundary of the location is within multiple time zones, the answer will return the time of the primary city within the location’s geographical boundary. 

###Weather Channel

######Description

######Actions

The weather channel provides weather information, for example temperature for a given location or forecast for a given location.

Action Name   |   Action Settings   |   Values   |   Examples  |
|------|------|------|-------|
   GetCurrentWeather    |   Location*     |   --   |   What is the weather in Seattle?    |
   GetCurrentTemperature   |   Location*    |   --   |   How cold is it in Munich?    |
   GetWeatherForecast   |    Location*, Date   |   ```{today|tomorrow|In2Days|In3Days|luis.buildin.date}```   |   Will it rain in Munich this evening? What is the weather forecast in Munich tomorrow?    |
   GetSunriseTime    |   Location*, Date    |   ```{Today|Tomorrow|luis.buildin.date }```   |   When is sunrise in Paris today?  |
   GetSunsetTime    |   Location*, Date   |   ```{Today|Tomorrow|luis.buildin.date }```   |   When is sunset in Paris today?   |

Prebuilt app: You can download a prebuilt app supporting our sample utterances for this action [here](https://www.luis.ai/Content/sampleApps/Build_Weather_v1.1.json).

######Additional Details

The weather zone channel returns the climate conditions of the given location. A location can be a city, a state, or a country. If a location is not known to the system, an error message will be returned by the action. There is a distinction between the current weather and forecasts for a given location. The current weather and temperature actions return data that represents the actual conditions, like current temperature, condition, wind directions and strength. You cannot specify a date or time for these values. The other intents use the forecast data and thus provide predicted data instead of actual values. Overview data (forecast summary) is available for the day and upcoming night of a specific date. The forecast range is limited to “today” and 6 days into the future. Any attempt to go beyond these boundaries will result in an error response. 
