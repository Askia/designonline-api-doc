# Changes
This section describes all changes in terms of feature development

## Question positioning fix
We fixed a bug about question positioning when manipulating them (moving, adding, deleting, inserting).

## userData is now exposed to AskiaScript
You can now acces the `userData` string of a question via AskiaScript

Create a question by providing a userData:
`POST /Questions/New`
```
{
    "mainCaption": "how old are you?",
    "type": "3",
    "shortcut": "age",
    "allowsNoResponse": false,
    "userData": "Slider"
}
```

Access the userData inside AskiaScript:
`age.userData`


You can also use `userData` to pass in a json object represented as a string
`POST /Questions/New`
```
{
    "mainCaption": "how old are you?",
    "type": "3",
    "shortcut": "age",
    "allowsNoResponse": false,
    "userData": "{\"type\" : \"slider\"}"
}
```

and parse that json string into a dictionary object in AskiaScript:

```
Dim dic as Dictionary
dic.LoadJSON(age.userData)
dic["slider"]
```

## Dynamic numeric error messages
The numeric error message is now dynamic and displays the min/max allowed values for the question

## Option to disable the browser validation for numerics
You can now disable the browser validation of numeric inputs by setting the `useBrowserValidation` extension property to 0 on the TemplateAll ADC.
You can do that either by calling a PUT method on the ADC Element of a specific question or by using the Default Controls feature we have in Design Online. 
The defaultControls can be set when creating a survey. Just provide the following `defaultControls` object into your json payload:

`POST {{url}}/AskiaPortal/Modules/design/api/Surveys/New?apiKey={{apiKey}}`

```
{
  "name": {{surveyName}},
  "defaultControls": {
    "3": {
      "controlId": 1,
      "properties": {
        "useBrowserValidation": 0
      }
    }
  }
}
```

In the `defaultControls` object `3` is the type of the question for which you want to provide a default control. `3` stands for numeric.

`controlId` is the id of the ADC. `1` stands for TemplateAll.

Finally we also provide a default value `0` to the `useBrowserValidation` property for this ADC.
In this example, from now on all numerics will use the TemplateAll ADC by default with this useBrowserValidation set to 0.

# Known issues

## Focus on previous button
When hitting the enter button while editing a numeric question the interview is headed back to the previous question
