<!-- 
NavPath: LUIS API
LinkLabel: Overview
Url: LUIS-api/documentation/home
Weight: 100
-->

#Overview

###Language Understanding Intelligent Services (LUIS) brings the power of machine learning to your apps

LUIS is designed to enable you to quickly deploy an HTTP endpoint that will take the sentences you send it and interpret them in terms of the intention they convey and the key entities that are present. By using the LUIS web interface, you can custom design a set of intentions and entities that are relevant to your application, then let LUIS guide you through the process of building a language understanding system. 

#####Benefits to using LUIS

One of the key problems in human-computer interactions is the ability of the computer to understand what a person wants, and to find the pieces of information that are relevant to their intent. For example, in a travel agent app, you might say "Book me a ticket to Paris" in which case there is the intention to "BookTicket" while "Paris" is the location entity. Intention can be defined as the desired action and usually contains a verb, in this case "book", and the entity is the topic/subject, in this case "Paris", of the action.

Once your application is deployed and traffic starts to flow into the system, LUIS uses active learning to improve itself. In the active learning process, LUIS identifies the interactions that it is relatively unsure of, and asks you to label them according to intent and entities. This has tremendous advantages, LUIS knows what it is unsure of, and asks you to help where you will provide the maximum improvement in system performance. Secondly, by focusing on the important cases, LUIS learns as quickly as possible, and takes the minimum amount of your time. This is [active machine learning](ActiveLearning.md) at its best.

#####Localization support 

The LUIS UI is always in English, but several languages such as English, French, Italian, Spanish, and Chinese are supported when it comes to understanding utterances. 

#####Accessing LUIS programmatically 

LUIS offers a programmatic REST API that can be used to automate the application creation process. This API allows you to author and publish your application by using LUIS endpoints. 

Click here for a complete [API reference](https://dev.projectoxford.ai/docs/services/56d95961e597ed0f04b76e58/operations/56f8a55119845511c81de488). 
