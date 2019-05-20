# Quick start

## Getting all surveys

The most basic operation you could do with the Design Online API is to fetch a list of your surveys.

Call the following API from any REST Client:

```
{{url}}/AskiaPortal/Modules/design/api/Surveys
```

`{{url}}` being the base url of your design online server instance.

and pass in the following HTTP header:

```
Cookie : {{cookie}}
```

`{{cookie}}` is the authentification cookie [you fetched in AskiaPortal](intro-authentification.md)

the complete request should look like this when called from cURL:

```shell
curl -X GET \
  http://localhost/AskiaPortal/Modules/design/api/Surveys \
  -H 'Cookie: whatever_cookie_value_you_have'
```

The server returns your list of basic survey objects inside a JSON Array :

```json
[
    {
        "defaultLanguageId": 2057,
        "defaultPageTemplateId": 1,
        "description": "",
        "id": 40,
        "name": "surveyTest"
    },
    {
        "defaultLanguageId": 2057,
        "defaultPageTemplateId": 1,
        "description": "",
        "id": 41,
        "name": "test2"
    },
    {
        "defaultLanguageId": 2057,
        "defaultPageTemplateId": 1,
        "description": "",
        "id": 42,
        "name": "PostmanSurvey"
    },
    {
        "defaultLanguageId": 2057,
        "defaultPageTemplateId": 1,
        "description": "",
        "id": 43,
        "name": "fromPM2"
    }
]
```

## Getting a specific survey  

You can also fetch a specific survey as long as you know its unique id. The server always returns more info when accessing a specific survey rather than the complete list of surveys. In the following call we are requesting the survey that has the id `42`

```shell
curl -X GET \
  https://alpha.askia.com/AskiaPortal/Modules/design/api/Surveys/42 \
  -H 'Cookie: whatever_cookie_value_you_have '
```

server's response:

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
    "id": 42,
    "languages": [
        2057
    ],
    "name": "PostmanSurvey",
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
