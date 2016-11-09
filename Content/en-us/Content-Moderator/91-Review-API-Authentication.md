<!-- 
NavPath: Content Moderator
LinkLabel: Review API Authentication
Url: content-moderator/documentation/review-api-authentication
Weight: 100
-->

# How to Authenticate Your Review API Calls #

## Introduction ##
The Review API is protected using Azure Active Directory. This section describes how you can generate the Azure Active Directory tokens to use for authenticating your review API calls.

## Where do I get my credentials? ##
Once you have created your team in the [review tool](http://contentmoderator.cognitive.microsoft.com/ "Content Moderator Review Tool"), navigate to the Settings page and select the API Tab.

## Client Id ##
You will find your Client Id listed on this page:
![API Settings](images/Review-API-Authentication-1A.png)

## Client Secret ##
The Keys portion of the Settings.API tab allows you to generate the client secrets(keys) that you would need to use to authenticate while using the Review API.

The secrets are time bound and can have lifetime of either 1 or 2 years. You can generate multiple secrets(keys) to cycle through them in your production environment.

The value of the secret(key) is viewable once after you generate it. So, please remember to save the value before navigating away from the page or before generating a new secret.

You can manage your existing secrets or create new ones from this page.
![API Settings](images/Review-API-Authentication-2A.png)

## Using the Client Id and Client Secret to Authenticate ##
Use the credentials generated on the Settings.API page to authenticate the Review API.

The following samples requests show how you will use you the Client Id and Client Secret(key) to generate time bound tokens.

## Request Samples ##

#### CURL ####
	curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d 'resource=https://api.contentmoderator.cognitive.microsoft.com/review&client_id=<Your Client Id>&client_secret=<Your Client Key/Secret>&grant_type=client_credentials' "https://login.microsoftonline.com/contentmoderator.onmicrosoft.com/oauth2/token"
 
	NodeJS Unirest
	var unirest = require("unirest");
	var req = unirest("POST", "https://login.microsoftonline.com/contentmoderator.onmicrosoft.com/oauth2/token");
 
	req.headers({
    	"content-type": "application/x-www-form-urlencoded"
	});
 
	req.form({
	  	"resource": "https://api.contentmoderator.cognitive.microsoft.com/review",
		"client_id": "< Your Client Id >",
		"client_secret": "< Your Client Key/Secret >",
	  	"grant_type": "client_credentials"
	});
 
	req.end(function (res){
		if (res.error) throw new Error(res.error);
		console.log(res.body);
	});
 
#### Python ####
	import http.client
	conn = http.client.HTTPSConnection("login.microsoftonline.com")
	payload = "resource=https%3A%2F%2Fapi.contentmoderator.cognitive.microsoft.com%2Freview&client_id=< Your Client Id >&client_secret=< Your Client Key/Secret >&grant_type=client_credentials"
	headers = {
    	'content-type': "application/x-www-form-urlencoded"
    }
	conn.request("POST", "/contentmoderator.onmicrosoft.com/oauth2/token", payload, headers)
	res = conn.getresponse()
	data = res.read()
	print(data.decode("utf-8"))

#### C# ####
	var client = new RestClient("https://login.microsoftonline.com/contentmoderator.onmicrosoft.com/oauth2/token");
	var request = new RestRequest(Method.POST);
	request.AddHeader("content-type", "application/x-www-form-urlencoded");
	request.AddParameter("application/x-www-form-urlencoded", "resource=https%3A%2F%2Fapi.contentmoderator.cognitive.microsoft.com%2Freview&client_id=< Your Client Id >&client_secret=< Your Client Key/Secret >&grant_type=client_credentials", ParameterType.RequestBody);
	IRestResponse response = client.Execute(request);

## Response Sample ##
	{
		"token_type": "Bearer",
		"expires_in": "3600",
		"ext_expires_in": "0",
		"expires_on": "1476491009",
		"not_before": "1476487109",
		"resource": "https://api.contentmoderator.cognitive.microsoft.com/review",
		"access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ikk2b0J3NFZ6QkhPcWxlR3JWMkFKZEE1RW1YYyIsImtpZCI6Ikk2b0J3NFZ6QkhPcWxlR3JWMkFKZEE1RW1YYyJ9.eyJhdWQiOiJodHRwOi8vd2ItcmV2aWV3LXN2YyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzdjNDZiZTcwLTkyZmItNDkzMS1hNzE5LWY0MWU4NmEwMGNlOS8iLCJpYXQiOjE0NzY0ODcxMDksIm5iZiI6MTQ3NjQ4NzEwOSwiZXhwIjoxNDc2NDkxMDA5LCJhcHBpZCI6IjIxMmQyODczLTFlZDEtNDRiNi1hNGFlLTQ1MWI4MjdmODZjZCIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzdjNDZiZTcwLTkyZmItNDkzMS1hNzE5LWY0MWU4NmEwMGNlOS8iLCJ0aWQiOiI3YzQ2YmU3MC05MmZiLTQ5MzEtYTcxOS1mNDFlODZhMDBjZTkiLCJ2ZXIiOiIxLjAifQ.jiCrnPMWDT0Zq9NPNjlU02-NeTNrOv13ujPODXvJ8Bvu5tRWKj4sjdHP-ml9L1KXgMUZZ_JZ9N7_7vFuard6hGg1XRE-ZeIuCToihy3M10kwaTEnNDQI4SRmuYWZZfhbEQ8FnSB5EICZnDKS5gFswkDVaQAjPSNKgV12fjIocqTxPvUpbDLYr8SPWcYuUitj803CPIpK9necLH7Fuh1Un2N_KJ9lPxvG5pbQRdUY4BIuKhuPOyFWx0_aAOSUZQx7xGOsL9VXKWg74elYOxcXL2gbqIEy1CA_tRyKhB_pJhB_4UcWpAEeP-v8ODpXiIqHWBuOImCarquGxY6STIaV1g"
	}

The POST token response specifies the token expiration detail. The expires_in property expresses the value in seconds. For example, the value "3600" denotes that the access token will expire in one hour from the time the response was generated. Partners may choose to cache the token until the token expiry time to avoid getting the token every time.
 
## Using the Token ##
You can now use the token while making the review API calls by sending the access_token in the header:

	Header name: authorization
	Header value: Bearer <Your access token>

## Helpful Links ##
[How to get an Azure AD security token](https://msdn.microsoft.com/en-us/library/partnercenter/dn974935.aspx "How to get an Azure AD token")
 





