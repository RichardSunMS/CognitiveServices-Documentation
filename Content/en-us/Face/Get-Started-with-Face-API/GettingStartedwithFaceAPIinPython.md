<!-- NavPath: Face API/Getting Started
LinkLabel: Get Started in Python
Url: face-api/documentation/get-started-with-face-api/GettingStartedwithFaceAPIinPython
Weight: 99
-->

# Getting Started with Face API in Python

In this tutorial, you will learn to invoke the Face API via the Python SDK to detect human faces in an image.

## Table of Contents

- [Preparation](#preparation)
- [Install Python SDK for the Face API](#sdk-install)
- [Subscribe for Face API and get your subscription key](#subscription)
- [Play with Python SDK to detect faces](#sdk-play)
- [Further Postprocess](#further)
- [Summary](#summary)
- [Related Topics](#related)

## <a name="preparation"></a> Preparation

To use the tutorial, you will need the following prerequisites:

- Python environment (Python 2.7+ and Python 3.5+ is recommended)

## <a name="sdk-install"></a> Install Python SDK for the Face API

```bash
pip install cognitive_face
```

## <a name="subscription"></a> Subscribe for Face API and get your subscription key

Before using any Face API, you must sign up to subscribe to Face API in the Microsoft Cognitive Services (formerly Project Oxford) portal. See [subscriptions](https://www.microsoft.com/cognitive-services/en-us/sign-up). Both primary and secondary key can be used in this tutorial.

## <a name="sdk-play"></a> Play with Python SDK to detect faces

```python
import cognitive_face as CF

KEY = 'subscription key'  # Replace with a valid Subscription Key here.
CF.Key.set(KEY)

img_url = 'https://raw.githubusercontent.com/Microsoft/Cognitive-Face-Windows/master/Data/detection1.jpg'
result = CF.face.detect(img_url)
print result
```

This code snippet should show something similar as following. It's a `list` of detected faces and each item is a `dict` instance where `faceId` is a unique ID of the detected face expired in 24 hours and `faceRectangle` describes the postion of the detected face.

```python
[{u'faceId': u'68a0f8cf-9dba-4a25-afb3-f9cdf57cca51', u'faceRectangle': {u'width': 89, u'top': 66, u'height': 89, u'left': 446}}]
```

## <a name='further'></a> Further Postprocess

For further postprocess, A GUI sample built with wxPython is also provided.  Before execution, please install [wxPython](https://wxpython.org/) as well as Python and the SDK metioned above.

```bash
git clone https://github.com/Microsoft/Cognitive-Face-Python.git
cd Cognitive-Face-Python
python sample
```

## <a name="summary"></a> Summary

In this tutorial, you have learned the basic process for using the Face API via invoking the Python SDK. For more information on API details, please refer to the How-To and [API Reference](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).

## <a name="related"></a> Related Topics

- [Getting Started with Face API in CSharp](GettingStartedwithFaceAPIinCSharp.md)
- [Getting Started with Face API in Java for Android](GettingStartedwithFaceAPIinJavaforAndroid.md)
