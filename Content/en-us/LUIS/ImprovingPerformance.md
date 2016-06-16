<!-- 
NavPath: LUIS API
LinkLabel: Improving Performance
Url: LUIS-api/documentation/ImprovingPerformance
Weight: 83 
-->

#Improving Performance of a LUIS Model

######There are several options for improving performance and resolving problems.

###Option 1: Adding model features

Behind the scenes, LUIS uses machine learning based methods to analyze sentences. This process is based on the presence or absence of clues, termed features, which are present in a sentence. For example, in the TravelAgent app, if the name of a city appears in an utterance, it is a good clue that the intent is to go to that city. 

You can give LUIS explicit knowledge about cities by creating a list that features them. To do this, click the **+** sign next to **Phrase List Features** on the lower left-hand menu panel. Name the feature "Cities", add the names of cities and travel destinations, and save it. LUIS will then be able to more easily recognize the BookTicket intent. 

![Phrase List](./Images/PhraseListCities.PNG)

As a second example, in the TravelAgent application, suppose people generally express the intent to book a trip by saying "Make a reservation ..." or "Book ticket to ...". Now suppose the system has received a request, "set me up to go to..." and labeled it as a **None** intent. The best thing to do would be to tell LUIS to treat the phrase "set me up to go to..." the same way it treats "Make a reservation..." or "Book ticket to...". This can be done by creating a phrase list feature called "BookItPhrases" and adding the mentioned three phrases. The "BookItPhrases" list will tell LUIS to treat these phrases as interchangeable. What LUIS learns about one phrase will automatically be applied to the others as well. 

Phrase list features work for both words and phrases. For example, if the phrase "tell me about" is important in an application, you could add it to a feature called SearchPhrases. A sequence of words separated by commas is treated as a phrase. 

Sometimes, it is easier to specify a regular expression (regex) than a list of phrases. For example, product codes might follow a regular pattern, like two letters followed by 3 digits. Regular expressions can be added by clicking on the **+** sign next to the **Regex Features** horizontal bar in the lower left-hand menu panel. The dialog that appears lists the regex instructions. 

######Adding model features is likely to help when...
  * The model fails to see that a class of words or phrases is similar, such as the names of cities or products. 
  * The model is having trouble identifying an entity. Adding a model feature with some or all of an entity's values often improves entity performance. 
  * The model is failing to act on rare or proprietary words. 

###Option 2: Add labeled utterances

Ultimately, the quality of the machine learning models depends on the quality and quantity of the labels. Adding more labeled utterances is a reliable way to improve performance. 

######Adding labeled utterances is likely to help when...
  * The model fails to differentiate between two different intents, using word patterns unlike those which have been labeled before. 
  * The model fails to recognize an entity based on words that surround it, like "search for trips to [city name]". 
  * The model erroneously and systematically assigns low scores to one intent. In this case, it may help to label more instances of this intent. 

###Option 3: Look for an incorrect utterance label

A common cause of error can be traced to a label that has been mis-assigned.

######It's worthwhile to look for an incorrect utterance label when...
  * The model fails to differentiate between two different intents, even though similar utterances have been labeled. 
  * An entity is consistently being missed, even though similar utterances have been labeled. 

###Option 4: Change the schema

Sometimes, the schema and the definitions of the intents and entities are too hard for a machine learning algorithm to learn. One indication is when it is difficult for the person doing the labeling to decide how to label utterances: if it's hard for a human, it's very hard for a machine! Changing the schema might mean combining, re-grouping, or dropping intents or entities. 

######As a last resort, consider changing the definition of the intents and entities when...
  * You often have difficulty deciding how to label utterances, and the model is performing poorly, despite having tried the three other options above. 
  

