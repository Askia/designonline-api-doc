# Creating a simple survey

This guide assumes that you have at least some experience with interacting with a REST API and that you have already read through the [Authentication section of this document](intro-authentification.md)

Note that all endpoints are rooted at `{{url}}`, which is the base url of the server on which your Design Online web application is running. For example, `https://alpha.askia.com`.

## Creating a survey

The easiest way to create a survey is to use a blank survey template. Predefined survey templates can be fetched through the `SurveyTemplate` endpoint.

```
{{url}}/AskiaPortal/Modules/design/api/SurveyTemplates
```
The server will return a list of existing `SurveyTemplate` objects
```json
[
    {
        "defaultLanguageId": 2057,
        "defaultPageTemplateId": 1,
        "description": "",
        "id": 1,
        "name": "Blank"
    }
]
```

We'll use the one and only predefined template of the list (the one with `id` = 1).

Let's now create our first survey by making a HTTP POST request to this endpoint:

```
POST {{url}}/AskiaPortal/Modules/design/api/Surveys/FromSurveyTemplate/{{survey_template_id}}
```

In our scenario the value of `survey_template_id` is `1` and the only data we will provide in the request body is the survey name. The request body:

```json
{
  "name": "FirstSurvey"
}
```
_Note: make sure to choose a survey name that is unique on the platform._

Because we are passing the body as JSON we have to let the server know about it. Just include the header `Content-Type: application/json` in your request.

The complete request can be called using cURL:

```shell
curl -X POST \
  https://alpha.askia.com/AskiaPortal/Modules/design/api/Surveys/FromSurveyTemplate/1 \
  -H 'Content-Type: application/json' \
  -H 'cookie: whatever_cookie_value_you_have' \
  -d '{ "name": "FirstSurvey" }'
```

The server returns the newly created survey. All survey properties will be set to default values specified in the survey template:

```json
{
    "defaultControls": {},
    "defaultLanguageId": 2057,
    "defaultPageTemplateId": 1,
    "defaultPageTemplateProperties": {
        "window_title": "Askia Web Survey",
        "survey_logo_src": "",
        "survey_logo_alt": "",
        "survey_name": "",
        "errors_caption": "",
        "display_progress_value": "yes",
        "sticky_header": "no",
        "radio_checkbox_size": "1.5rem",
        "ribbon_footer_background_color": "{%= Theme.PrimaryColor %}",
        "buttons_alignement": "center",
        "display_previous": "yes",
        "previous_caption": "Previous",
        "next_caption": "Next",
        "display_footer": "yes",
        "footer_left": "",
        "footer_right": ""
    },
    "description": "",
    "id": 99,
    "languages": [
        2057
    ],
    "name": "FirstSurvey",
    "themeProperties": {
        "fontFamily": "Arial, Helvetica, sans-serif",
        "baseFS": "16px",
        "largeFS": "1.5rem",
        "normalFS": "1.05rem",
        "smallFS": "0.85rem",
        "lineHeight": "1.2",
        "borderWidth": "0.0625em",
        "borderRadius": "0.1875em",
        "hPadding": "1.0em",
        "vPadding": "1.0em",
        "whiteColor": "255,255,255,1",
        "blackColor": "34,34,34,1",
        "primaryColor": "40,59,73,1",
        "primaryDarkColor": "25,39,48,1",
        "primaryLightColor": "72,101,121,1",
        "secondaryColor": "223,67,53,1",
        "secondaryDarkColor": "175,36,23,1",
        "secondaryLightColor": "240,120,109,1",
        "neutralColor": "221,221,221,1",
        "neutralDarkColor": "170,170,170,1",
        "neutralLightColor": "238,238,238,1",
        "errorColor": "192,57,43,1",
        "successColor": "1681901197"
    }
}
```

## Providing more properties on survey creation 

When creating a survey you can pass in more survey properties. In  this example we'll provide a JSON payload with some extra properties:

```json
{
  "name": "SurveyWithMoreAttributes",
  "description": "cool survey",
  "languages": [1036],
  "themeProperties": {
    "borderWidth": "1px",
    "borderRadius": "0.1875em",
    "errorColor": "255,255,102"
  }
}
```

In this example we are creating a new survey with a description, a language set to French and some values for certain properties of the survey's theme.

The complete cURL command:
```shell
curl -X POST \
  https://alpha.askia.com/AskiaPortal/Modules/design/api/Surveys/FromSurveyTemplate/1 \
  -H 'Content-Type: application/json' \
  -H 'cookie: whatever_cookie_value_you_have' \
  -d '{
	"name": "SurveyWithMoreAttributes",
	"description": "cool survey",
	"languages": [1036],
	"themeProperties": {
	  "borderWidth": "1px",
          "borderRadius": "0.1875em",
	  "errorColor": "255,255,102"
  }
}'
```

## Adding questions to a survey
Once a survey is created you can add questions and responses in a few steps.

To create a question, call the following endpoint with a POST HTTP request:
```
{{url}}/AskiaPortal/Modules/design/api/Surveys/{{surveyId}}/Questions/New
```

where `{{surveyId}}` is the value of the `id` property of the survey in the earlier response.

You can of course pass in question properties in the JSON request. For a full list of properties and an explanation of their meaning and acceptable values, have a look at our [API reference](api-reference-intro.md)):

```json
{
  "allowsNoResponse": false,
  "mainCaption": "Are you a man or a woman <img src=\"https://www.jquery-az.com/html/images/banana.jpg\" height=\"42\" width=\"42\"/>",
  "rotationType": 2,
  "shortcut": "q1_gender",
  "type": 1
}
```
With this request we are asking the server to create a question with the following properties: 

* The respondent must answer the question (by providing a value of `false` to `allowsNoResponse`) 
* The question is a closed question of which only one response can be chosen (by providing a value of `1` for `type` which is is the value for a closed question that allows only one response).
* The `rotationType` of the question is set to `2` and this stands for 'circular rotation'.
* There is a unique identifier - 'shortcut' - of `q1_gender`
* The full text of the question when presented to the respondent is formatted with HTML by setting the value of the `mainCaption`

Note that the `mainCaption`is a plain HTML text field and you can reference any external or internal images as in any other HTML content.

Here is the cURL request:
```shell
curl -X POST \
  'http://{{url}}/AskiaPortal/Modules/design/api/Surveys/{{surveyId}}/Questions/New' \
  -H 'Content-Type: application/json' \
  -H 'cookie: {whatever_cookie_value_you_have}' \
  -d '{
  "allowsNoResponse": false,
  "mainCaption": "Are you a man or a woman? <img src=\"https://www.jquery-az.com/html/images/banana.jpg\" height=\"42\" width=\"42\"/>",
  "rotationType": 2,
  "shortcut": "q1_gender",
  "type": 1
}'
```
the server's response should have a HTTP `200` status code with the newly created question object.
```json
{
    "allowsNoResponse": false,
    "alwaysLinkExclusiveResponses": false,
    "analyseCaption": "",
    "anonymisationType": 0,
    "categories": [],
    "decimalPrecision": 0,
    "firstChildId": null,
    "id": 4,
    "impClosedMatchingType": 0,
    "impDatabaseDsn": "",
    "impFieldName": "",
    "impIsInvisibleWhenImported": false,
    "impPanelUpdateType": 0,
    "impSqlQuery": "",
    "impType": 0,
    "isDeleted": null,
    "isExcludedFromTranslation": true,
    "isFirstInPage": true,
    "isLastInPage": true,
    "isLevelDeveloped": true,
    "isLevelLinked": false,
    "isProbability": false,
    "isRanked": false,
    "isRecordable": false,
    "isScaled": false,
    "isVisibleInAnalyse": true,
    "ivrNumber": "",
    "lastChildId": null,
    "linkedQuestionId": null,
    "linkType": 0,
    "mainCaption": "Are you a man or a woman? <img src=\"https://www.jquery-az.com/html/images/banana.jpg\" height=\"42\" width=\"42\"/>",
    "maxResponseCount": null,
    "maxValue": null,
    "maxVisibleResponses": "",
    "mergingPageId": null,
    "minResponseCount": null,
    "minValue": null,
    "nextSiblingId": null,
    "noResponseEntry": "",
    "parentId": null,
    "pattern": "",
    "position": 3,
    "prevSiblingId": 2,
    "questionIdToIncrement": 0,
    "rotationSeed": null,
    "rotationType": 2,
    "shortcut": "q1_gender",
    "type": 1,
    "userData": "",
    "visibility": 0
}
```
Let's repeat that for a question 2 and 3

```shell
curl -X POST \
  https://alpha.askia.com/AskiaPortal/Modules/design/api/Surveys/{{survey_id}}/Questions/New \
  -H 'Content-Type: application/json' \
  -H 'cookie: {whatever_cookie_value_you_have}' \
  -d '{
  "shortcut": "q2_female",
  "type": 1,
  "mainCaption" : "From postman: Question for a woman?"
}'
```

```shell
curl -X POST \
  https://alpha.askia.com/AskiaPortal/Modules/design/api/Surveys/{{survey_id}}/Questions/New \
  -H 'Content-Type: application/json' \
  -H 'cookie: {whatever_cookie_value_you_have}' \
  -d '{
  "shortcut": "q2_male",
  "type": 1,
  "mainCaption" : "From postman: Question for a man?"
}'
```

## Adding responses  
At this point if you fetch the list of questions for your survey you'll receive a JSON array of three questions. Let's add two responses for the first question, to which we gave the shortcut `q1_gender`.

We will be calling the following endpoint to the responses in the body:
```
POST AskiaPortal/Modules/design/api/Surveys/{{surveyId}}/Questions/{{question_id}}/Responses
```
`question_id` is of course the `id` of the question returned by the server when it was created.

The JSON content is straightforward:
```json
[
  {
    "mainCaption": "Man : <img src=\"https://your_server/man.jpg\" height=\"42\" width=\"42\"/>"
  },
  {
    "mainCaption": "Woman : <img src=\"https://your_server/woman.jpg\" height=\"42\" width=\"42\"/>"
  }
]
```

If you receive a `200` status code and the following JSON (which is an array of response objects), everything has worked as expected.
```json
[
    {
        "baseType": 0,
        "entryCode": "",
        "factor": null,
        "firstChildId": null,
        "id": 4,
        "isDeleted": null,
        "isExcludedFromTranslation": false,
        "isExclusive": false,
        "isSelectable": true,
        "lastChildId": null,
        "mainCaption": "Man : <img src=\"https://your_server/man.jpg\" height=\"42\" width=\"42\"/>",
        "nextSiblingId": 5,
        "parentId": null,
        "position": 3,
        "prevSiblingId": 3,
        "questionId": 1,
        "resourceId": null,
        "rotationBehaviour": 0,
        "semiOpenQuestionId": null,
        "type": 0,
        "userData": ""
    },
    {
        "baseType": 0,
        "entryCode": "",
        "factor": null,
        "firstChildId": null,
        "id": 5,
        "isDeleted": null,
        "isExcludedFromTranslation": false,
        "isExclusive": false,
        "isSelectable": true,
        "lastChildId": null,
        "mainCaption": "Woman : <img src=\"https://your_server/woman.jpg\" height=\"42\" width=\"42\"/>",
        "nextSiblingId": null,
        "parentId": null,
        "position": 4,
        "prevSiblingId": 4,
        "questionId": 1,
        "resourceId": null,
        "rotationBehaviour": 0,
        "semiOpenQuestionId": null,
        "type": 0,
        "userData": ""
    }
]
```

You've now finished this tutorial on how to create basic questions and answers. Feel free to play with the API and experiment with other properties to pass in your questions and responses requests. At any point you can call the test endpoint `{{url}}/AskiaPortal/Modules/design/api/Test/Survey/{surveyId}` in a browser and have a test view of your survey.

Next read our [Routings Guide](guide-routings.md)
