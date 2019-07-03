# Changes
This section describes all changes in terms of feature development

## Interview resources fix
When published to a live environnement an interview has now access to its resources (images, look and feel, ADC...)


## Import parameters
When a survey is live and opened via the user link query string parameters can be imported and set as data for specific questions.

Consider this live survey link:  
`{{AskiaExtURL}}?Action=DoExternalPanel&SurveyName={survey_name}&Broker={BROKER}&BrokerPanelId={BROKERPANELID}&paramToBeImported={param}`

To set the import option on a question (in order to import `paramToBeImported`) you'll have to create the question (or update it) with the following paylod:

```
  {"impType":5,"impFieldName":"paramToBeImported"}
```

- impType: is the Type of the import, 5 stands for "Internet parameters" aka know as url query strings
- impFieldName: is the name of the internet parameter


# Known blocking issues

## Phantom objects
 - Sometimes objects like Responses are visibles in the web interface but not on the test link (and they disappear from the web interface if you recycle the app in IIS)

 - An object creation (Routing) might fail through the API, but the object is created anyway in memory/cache and visible on the web interface.

## Error messages
We are working on a way to let users define basic and localized error messages on surveys
