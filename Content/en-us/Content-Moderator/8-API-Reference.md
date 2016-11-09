<!-- 
NavPath: Content Moderator
LinkLabel: API Reference
Url: content-moderator/documentation/api-reference
Weight: 130
-->

# API Reference #

## Review API ##
Use this API to integrate your content (images) after you have signed up for the [review tool](http://contentmoderator.cognitive.microsoft.com/ "Content Moderator Review Tool"). The review tool will internally use the Moderate APIs to scan your images, and create reviews in the review tool to be available for human moderation team for taking actions.

[**Review API**](https://westus.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/580519483f9b0709fc47f9c5 "Content Moderator Review API")

## Moderate API ##
Use the image and text moderation operations to scan your content. You can get access to the free tier (5K transactions per month) by signing up for the review tool. You will find your Moderate API credentials listed within the "API" section under Settings in the review tool.

The API will moderate your content and send the results with relevant information either back to your systems or to the built-in review tool (for images), depending on who is calling the API. You can use this information to implement your own post-moderation workflow such as publish, reject, or review.

[**Image and Text Moderation APIs**](https://westus.dev.cognitive.microsoft.com/docs/services/57cf753a3f9b070c105bd2c1/operations/57cf753a3f9b070868a1f66c "Image and Text Moderation APIs")

## List Management API ##
Use this API to create and manage your custom lists of Images and Text. The lists that you create can be used in the **Image/Match** and **Text/Screen** operations. You can use your Moderate API credentials for the list management API as well.

[**List Management API**](https://westus.dev.cognitive.microsoft.com/docs/services/57cf755e3f9b070c105bd2c2/operations/57cf755e3f9b070868a1f675 "Content Moderator List Management API")
