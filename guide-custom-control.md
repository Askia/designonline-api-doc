# Using custom controls

This guide is assuming you have at least some experience with interacting with a REST api and that you already had a look at the [Authentification section of this document](intro-authentification.md)

This guide will start right where the one on [Creating a survey](guide-create-survey.md) ends.
If you did not follow this guide, you'll need to create a survey, add at least 1 single answer question with two responses.

**Note: This API is a work in progress and there is a good chance the routes described in this guide will be revamped and simplified in the near future**

## Fetching custom controls

Surveys created from the DesignOnline API can be customized. In this guide we will customize a single answer question and transform the user input to a dropdown in the survey.

All Askia Design Controls are open sourced and can be found on [Github](https://github.com/AskiaADX)
These controls come natively with the Design Online API.

Fetching the control list from the API `GET /api/Controls` returns an array of all available controls.

```json
[
  {
    "allowedQuestionTypes": [
      1,
      2,
      3,
      5,
      4
    ],
    "id": 1,
    "name": "TemplateAll",
    "properties": [
      {
        "defaultValue": "center",
        "description": "The alignment of the control]",
        "group": "General",
        "id": "controlAlign",
        "name": "Control Alignment",
        ...
      },
      {...}
    ]
  },
  {...}
]
```

Each control comes with an array of compatible [QuestionTypes](http://installers.askia.com/helpdesk/devs/AskiaCoreDoc/html/79108644-24ea-a2e7-b662-59e882cdf1e3.htm).

In this guide we are going to use the `TemplateAll` control (id = 1) and set it as the main control of our question.

## Question Architecture

In a survey each question has a specific style. A style is defined by a tree of `Elements` with each `Element` representing a UI component for the question.

This is a representation of the Element tree for a given question:

- Page (Element Type: 0)
    - Main Container(Element Type: 1)
      - Question Container (Element Type: 2)
          - Caption (Element Type: 3)
          - Control (Element Type: 4)


To set a custom control for a question, you'll need to alter the Control Element inside the question's style.

## Finding the right Element

Let's start by fetching the right UI Element for our question.

`GET /api/Surveys/{surveyId}/Elements/ContainsQuestion/{questionId}`

This endpoint returns the question's element tree as a JSON array:
```json
[
  {
    ...
    "id": 9,
    "type": 0 // page element
  },
  {
    ...
    "id": 10,
    "type": 2 //Question container element
  },
  {
    ...
    "id": 11,
    "type": 3 //Caption element
  },
  {
    ...
    "id": 12,
    "type": 4 //Control element
  }
]
```

The id of the UI element we need to alter is 12 as it types is 4 (which is the type of all Control Elements)

Let's now alter this specific element using the API and passing in the Id of the custom Control we fetched earlier (id : 1)

`PUT /api/Surveys/{surveyId}/Elements/{elementId}`

where surveyId is the id of our survey and elementId the Id of the UI element fetched earlier, the one with an element type of 4 (that id would be 12 in our example).

We have to pass in the json payload inorder to update our element with the new controlId :
```json
{
  "controlId": 1, //The id of our control choosen from the available controls
  "extensionProperties": {"useList": "1"} //some control specific properties (here we are using the control as a clmosed question dropdown)
}
```

You should get a 200 status code from the server and a full json object representing your updated UI element:
```json
{
  "afterEnd": "",
  "afterStart": "",
  "attributes": "",
  "beforeEnd": "",
  "beforeStart": "",
  "classes": "",
  "controlId": 1,
  "extensionProperties": {
    "controlAlign": "center",
    "placeholder": "",
    "autoSubmit": "no",
    "maxWidth": "100%",
    "columnsCount": "1",
    "columnsWidth": "200px",
    "useList": "1",
    "firstOptionText": "",
    "numUseInput": "0",
    "unitStep": "1",
    "numBoxPrefix": "",
    "numBoxSuffix": "",
    "numDkButton": "0",
    "numDkCaption": "Don't know",
    "opensubtype": "text",
    "openDkButton": "0",
    "openDkCaption": "Don't know",
    "theme": "light-theme",
    "defaultDate": "",
    "bound": "1",
    "position": "bottom left",
    "setDefaultDate": "0",
    "firstDay": "1",
    "disableWeekends": "1",
    "showWeekNumber": "0",
    "showMonthAfterYear": "0",
    "numberOfMonths": "1",
    "mainCalendar": "left",
    "dateDkButton": "0",
    "dateDkCaption": "Don't know",
    "imperial": "false",
    "showSeconds": "false",
    "stepMinutes": "1",
    "stepSeconds": "1"
  },
  "firstChildId": null,
  "id": 4,
  "isDeleted": false,
  "lastChildId": null,
  "nextSiblingId": null,
  "pageTemplateId": null,
  "parentId": 2,
  "position": 1,
  "prevSiblingId": 3,
  "questionId": 1,
  "style": "",
  "type": 4
}```

You can now test your survey and confirm that your user input is a dropdown instead of two radio buttons.

![dropdown](https://github.com/Askia/designonline-api-doc/blob/master/assets/dropdown.png)
