# Creating a simple survey with basic Routing (survey logic)

This guide is assuming you have at least some experience with interacting with a REST api and that you alreay had a look at the [Authentification section of this document](intro-authentification.md)

## Creating a survey

The easiest way to create a survey is to use a blank survey template. Predefined survey templates can be fetched through the SurveyTemplate Route.

```
{{url}}/AskiaPortal/Modules/design/api/SurveyTemplates

```
The server will return a list of existing SurveyTemplates
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

We'll use the one and only predefined template of the list (the one with id = 1).
Let's now create our first survey using this handy endpoint which we will call using a POST http method:

```
POST {{url}}/AskiaPortal/Modules/design/api/Surveys/FromSurveyTemplate/{{survey_template_id}}
```

`{{url}}` being the base url of your design online server instance.

In our scenario survey_template_id is 1 and the only input data we need to provide (in the request body) for now is the survey name. The request body:

```json
{
	"name": "FirstSurvey"
}
```
Make sure to choose a survey name that is unique through the platform.  
Because we are passing the body as a json payload we have to let the server know about it. Just pass the`Content-Type: application/json` header to your request.

The complete request can be called using cURL:

```shell
curl -X POST \
  https://alpha.askia.com/AskiaPortal/Modules/design/api/Surveys/FromSurveyTemplate/1 \
  -H 'Content-Type: application/json' \
  -H 'cookie: whatever_cookie_value_you_have' \
  -d '{
	"name": "FirstSurvey"
}'
```

The server returns your newly created survey with the data provided. All other survey properties will be set to defaults values:

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

## Providing more survey parameters  

When creating a survey you can pass in more survey data. In  this example we'll provide a json payload with some extra parameters:

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

In this example we are creating a new survey with a description, a language set to French and some default theme properties.

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

## Adding questions and responses to the survey
