<!-- 
NavPath: Content Moderator
LinkLabel: Get Started
Url: content-moderator/documentation/quickstart
Weight: 190
-->

# Get Started #
Start by signing up for the [**review tool**](http://contentmoderator.cognitive.microsoft.com/ "Content Moderator Review Tool") and uploading images to explore the automated moderation and review the  results right within your web browser. You can take actions such as changing the highlighted tags and submitting your decisions to the default workflow. You can then move on to using the review API to integrate your content (images) with the tool, and finally, use the underlying moderation APIs directly for automated moderation and custom list management.

## 1. Sign up for the review tool ##
Sign up to try the [**review tool**](http://contentmoderator.cognitive.microsoft.com/ "Content Moderator Review Tool") by either using your existing Microsoft account or create a new account within the review tool.

## 2. Invite team members ##
On the opening screen after signup, name your team, and optionally, invite your colleagues by entering their email addresses. You can see the status of existing invites, cancel pending invites, and after confirmation by the invited users, you can assign them the role of an administrator (like yourself) or of a reviewer.

![Invite team member](images/QuickStart-2-small.png)

## 3. Upload images ##
Use the File Upload feature to upload a set of sample images for moderation. These can be your images, subject to size and count restrictions. You will find a link to download the sample images on the File Upload screen.

![Upload files](images/QuickStart-3.PNG)

## 4. Start automated moderation ##
Submit your uploaded content to start the auto-moderation step. Internally, the review tool will call the moderation APIs to scan your content for built-in tags. Once the scanning is complete, you will see a message informing you about the results waiting for your review.

![Moderate files](images/QuickStart-4.PNG)

## 5. Review moderation results ##
As your business application calls the Moderator API, the tagged content will start queuing up, ready to be reviewed by the human review teams. You can quickly review large volumes of content using this approach. You will be doing a few different things as part of your moderation workflow such as:

- Adjusting the zoom level
- Browsing the reviews on-screen
- Reviewing moderation scores and results
- Confirming or modifying the tags returned by the API

![Review results](images/QuickStart-5.PNG)

## 6. Integrate with the review tool by using the review API ##
Once you have explored the review tool, use the [**review API**](https://westus.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/580519483f9b0709fc47f9c5 "Content Moderator Review API") to integrate large number of images with the review tool in an automated way. The review API will scan your images and generate reviews in the review tool where you can resume the human review steps.

## 7. Directly use the Moderate APIs for image and text moderation ##
Use the [**image and text moderation APIs**](https://westus.dev.cognitive.microsoft.com/docs/services/57cf753a3f9b070c105bd2c1/operations/57cf753a3f9b070868a1f66c "Content Moderator Moderate APIs") to directly scan your content and get back the detailed results You can use the information to either implement your post-moderation workflow by either using your  systems and/or create reviews within the built-in review tool for your human moderation teams. You will find your Moderate API credentials listed within the "API" section under Settings in the review tool.

## 8. Create and manage custom lists of content ##
Enhance your moderation effectiveness by using the [**list management API**](https://westus.dev.cognitive.microsoft.com/docs/services/57cf755e3f9b070c105bd2c2/operations/57cf755e3f9b070868a1f675 "Content Moderator List Management API") to create and manage custom lists of known (approved and blocked) text and images to the incoming content before moderating. The lists that you create can be used in the Moderate operations. You can use your Moderate API credentials for the list management API as well.
