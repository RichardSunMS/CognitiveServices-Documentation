<!-- 
NavPath: Face API
LinkLabel: Overview
Url: face-api/documentation/overview
Weight: 100
-->
# Face API

Welcome to the Microsoft Face API, a cloud-based service that provides the most advanced face algorithms. Face API has two main functions: face detection with attributes and face recognition.

## Face Detection

Face API detects up to 64 human faces with high precision face location in an image. And the image can be specified by file in bytes or valid URL.

![Overview - Face Detection](./Images/Face.detection.jpg)

Face rectangle (left, top, width and height) indicating the face location in the image is returned along with each detected face. Optionally, face detection extracts a series of face related attributes such as pose, gender, age, head pose, facial hair and glasses. Refer to [Face - Detect](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236) for more details.

## Face Recognition

Face recognition is widely used in many scenarios including security, natural user interface, image content analysis and management, mobile apps, and robotics. Four face recognition functions are provided: face verification, finding similar faces, face grouping, and person identification.


### Face Verification

Face API verification performs an authentication against two detected faces or authentication from one detected face to one person object. Refer to [Face - Verify](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523a) for more details.

### Finding Similar Face

Given target detected face and a set of candidate faces to search with, our service finds a small set of faces that look most similar to the target face. Two working modes, `matchFace` and `matchPerson` are supported. `matchPerson` mode returns similar faces after applying a same-person threshold derived from [Face - Verify](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523a). `matchFace` mode ignores the same-person threshold and returns top similar candidate faces. Take the following example, candidate faces are listed.      
![Overview - Face Find Similar](./Images/FaceFindSimilar.Candidates.jpg)
And query face is 

![Overview - Face Find Similar](./Images/FaceFindSimilar.QueryFace.jpg) 

To find 4 similar faces, `matchPerson` mode returns (a) and (b), which belong to the same person with query face. `matchFace` mode returns (a), (b), (c) and (d), exactly 4 candidates even if low similarity. Refer to [Face - Find Similar](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395237) for more details.

### Face Grouping

Given one set of unknown faces, face grouping API automatically divides them into several groups based on similarity. Each group is a disjointed proper subset of the original unknown face set, and contains similar faces. And all the faces in the same group can be considered to belong to the same person object. Refer to [Face - Group](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395238) for more details.

### Face Identification

Face API can be used to identify people based on a detected face and people database (defined as a person group) which needs to be created in advance and can be edited over time.

The following figure is an example of a person group named "myfriends". Each group may contain up to 1,000 person objects. Meanwhile, each person object can have one or more faces registered. 

![Overview - Person Group](./Images/person.group.clare.jpg)

After a person group has been created and trained, identification can be performed against the group and a new detected face. If the face is identified as a person object in the group, the person object will be returned.

For more details about person identification, please refer to the API guides listed below:

[Face - Identify](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239)  
[Person Group - Create a Person Group](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395244)  
[Person - Create a Person](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523c)  
[Person Group - Train Person Group](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395249) 

### Face Storage 
Face Storage allows a Standard subscription to store additional persisted faces when using Person objects ([Person - Add A Person Face](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523b)) or Face Lists ([Face List - Add a Face to a Face List](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395250)) for identification or similarity matching with the Face API. The stored images are charged at $0.5 per 1000 faces and this rate is prorated on a daily basis. Free tier subscriptions are free, but limited to 1,000 total persons. 

Pricing for Face Storage is prorated daily. For example, if your account used 10,000 persisted faces each day for the first half of the month and none the second half, you would be billed only for the 10,000 faces for the days stored. Alternatively, if each day during the month you persist 1,000 faces for a few hours and then delete them each night, you would still be billed for 1,000 persisted faces each day.



## Changes

This document is targeting **Microsoft Face API** service version 1.0.

### Release changes in November 2016

* **Face Storage expansion** Face Storage allows a Standard subscription to store additional persisted faces when using Person objects ([Person - Add A Person Face](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523b)) or Face Lists ([Face List - Add a Face to a Face List](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395250)) for identification or similarity matching with the Face API. The stored images are charged at $0.5 per 1000 faces and this rate is prorated on a daily basis. Free tier subscriptions continue to be limited to 1,000 total persons. 

### Release changes in October 2016

* **Error Message Change** In [Face List - Add a Face to a Face List](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395250) and [Person - Add a Person Face](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523b) APIs, the error message of more than 1 face in the `targetFace` changes from `There are more than 1 face in the image` to `There is more than 1 face in the image`.

### Release changes in July 2016

* **Face Verification API** Face to Person object authentication is supported – previously Face Verification requests only supported Face to Face authentication. More details can be found: [Face - Verify](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523a).

* **Finding Similar Face API** Added optional `mode` field enabling selection of two working modes, default `matchPerson` works the same as before, and new mode `matchFace` removes the same person filtering. If `mode` field is not specified, the behavior is the same as the past release. More details can be found: [Face - Find Similar](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395237).

* **Face Identification API** Optional user-specified `confidenceThreshold` is enabled for user to define the confidence threshold of whether one face belong to a person object. More details can be found: [Face - Identify](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239).

* **List person groups** New optional `start` and `top` parameters in list person groups to support user specifying the start point and the total person groups number to list. More details can be found: [Person Group - List Person Groups](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395248).

**Note**: All of these changes are compatible with the last version service, and using the default value for the newly added parameters will not cause any changes to users' code. 

### V1.0 changes from V0

* **API Signature**
In Face API V1.0, Service root endpoint changes from `https://api.projectoxford.ai/face/v0/` to `https://api.projectoxford.ai/face/v1.0/` 
There are several signature changes for API, such as [Face - Detect](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236), [Face - Identify](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239), [Face - Find Similar](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395237), [Face - Group](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395238).

* **Face sizes**
The previous version of Face API was not clear about the smallest face sizes the API could detect. With V1.0 the API correctly sets the minimal detectable size to 36x36 pixels. Faces smaller 36x36 pixels will not be detected.

* **Persisted data**
Existing Person Group and Person data which has been setup with Face V0 cannot be accessed with the Face V1.0 service. This incompatible issue will occur for only this one time, following API updates will not affect persisted data any more.

* **Note**: The V0 endpoint of Face API was retired on **06/30/2016**.

## Getting Started

To quickly go through the Face API basic functionalities and subscriptions processes, please refer to our get started tutorials.

- [Getting Started with Face API in CSharp](Get-Started-with-Face-API/GettingStartedwithFaceAPIinCSharp.md)
- [Getting Started with Face API in Java for Android](Get-Started-with-Face-API/GettingStartedwithFaceAPIinJavaforAndroid.md)
- [Getting Started with Face API in Python](Get-Started-with-Face-API/GettingStartedwithFaceAPIinPython.md)

## Sample Apps
Take a look at these sample applications which make use of Face API.

- [FamilyNotes UWP app](https://github.com/Microsoft/Windows-appsample-familynotes)
 - Universal Windows Platform (UWP) sample app that shows usage of speech, Cortana, ink, and camera through a family note sharing scenario. 
- [Video Frame Analysis Sample](https://github.com/microsoft/cognitive-samples-videoframeanalysis)
 - Universal Windows Platform (UWP) sample app that shows analyzing live video streams in near real-time using the Face, Computer Vision, and Emotion APIs.

## Related Topics

- [How to Detect Faces in Image](Face-API-How-to-Topics/HowtoDetectFacesinImage.md)
- [How to Identify Faces in Image](Face-API-How-to-Topics/HowtoIdentifyFacesinImage.md)
