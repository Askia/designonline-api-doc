# Changes
This section describes all changes in terms of feature development

## Publish feature

The Design Online API has now a publish endpoint. The goal of this endpoint is to send the survey to the field part of Askia.
You can publish a survey by calling:
```
POST {{url}}/AskiaPortal/Modules/design/api/surveys/{{surveyId}}/Publish?apikey={{apiKey}}
```

This api call does not require any body to be included for now.

The **Design server** will publish the survey to our **Field server** and retrieve it's SurveyTask id (along other attributes) and forward it to you as a response to the call you made.


Response example:
```
{
    "dateCreated": "2019-06-27T15:47:11.7",
    "dateModified": "2019-06-27T15:47:14.518",
    "description": "",
    "name": "TestSurvey",
    "serverId": 3,
    "surveyTaskId": 1243,
    "webProdUrl": null
}
```


**Important Note:**
At this stage your survey is in the Field server but is not available to users yet. You'll need to set it **online**.

Setting a survey online/offline is done by using our Field API called [CcaWebAPI](http://10.0.51.62/ccawebapi).

You'll need to call:
```
PUT  {{fieldUrl}}/SurveyTasks/{id}/WebConnections/{webConnectionId}
```
- id: the SurveyTask id you got previously when calling the publish endpoint
- webConnectionId: you can use 1 for now.

And provide a json paylod in the body:
```
{
  "Online": true
}
```

**Note:**  The field API needs authentication as well:
Pass an `Authorization` header on the request with the value: `Basic {token}`

**Please contact us to get a valid token**


Once your survey is online you can simply start an interview by using for example the DoExternalPanel link:

`{{fieldURl}}/WebProd/cgi-bin/askiaext.dll?Action=DoExternalPanel&SurveyName={{your_surveyName}}&Broker={your_broker_name}&BrokerPanelId={your_broker_panel_id}`

# Known blocking issues

## Survey Look & Feel in production
When the survey is published and set online, it will loose it's html assets path and therefor its look and feel is broken.

## Phantom objects
 - Sometimes objects like Responses are visibles in the web interface but not on the test link (and they disappear from the web interface if you recycle the app in IIS)

 - An object creation (Routing) might fail through the API, but the object is created anyway in memory/cache and visible on the web interface.

## Error messages
We are working on a way to let users define basic and localized error messages on surveys
