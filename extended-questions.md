** Read

You can get all questions GET api/Surveys/2/ExtendedQuesions

Response output

```json
[
  {
      "id":22,
      "type":1,
      "controlId":31,
      "controlProperties":{
         "controlAlign":"left",
         ...andTheOtherControlProperties
      },
      "responses":[
         {
            "id":67,
            "mainCaption":"male",
            ...andTheOtherResponseProperties
         },
         {
            "id":68,
            "mainCaption":"female",
            ...andTheOtherResponseProperties
         }
      ],
      ...andTheOtherQuestionProperties
  }
]
```

Or you can get one specific question GET api/Surveys/2/ExtendedQuesions/22

Response output
```json
  {
      "id":22,
      "type":1,
      "controlId":31,
      "controlProperties":{
         "controlAlign":"left",
         ...andTheOtherControlProperties
      },
      "responses":[
         {
            "id":67,
            "mainCaption":"male",
            ...andTheOtherResponseProperties
         },
         {
            "id":68,
            "mainCaption":"female",
            ...andTheOtherResponseProperties
         }
      ],
      ...andTheOtherQuestionProperties
  }
```json
Create
Request input

// POST api/Surveys/2/ExtendedQuesions/New
{
  "shortcut": "gender",
  "type": 1,
  "controlId": 31,
  "controlProperties": {
    "controlAlign": "left"
  },
  "responses": [
    {
      "mainCaption": "male"
    },
    {
      "mainCaption": "female"
    }
  ]
}
Response output

{
    "id":22,
    "type":1,
    "controlId":31,
    "controlProperties":{
       "controlAlign":"left",
       ...andTheOtherControlProperties
    },
    "responses":[
       {
          "id":67,
          "mainCaption":"male",
          ...andTheOtherResponseProperties
       },
       {
          "id":68,
          "mainCaption":"female",
          ...andTheOtherResponseProperties
       }
    ],
    ...andTheOtherQuestionProperties
}
Update
Request input

NOTE: The response field does not handle the response ordering.
Created responses are added at the end of the list of existing responses.
Updated responses will not be moved.

// PUT api/Surveys/2/ExtendedQuesions/22
{
  "shortcut": "gender renamed",
  "type": 1,
  "controlId": 31,
  "controlProperties": {
    "controlAlign": "left"
  },
  "responses": [
    // adds response by omitting the id field 
    {
      "mainCaption": "other"
    },
    // updates response by specifying the id field
    {
      "id": 67,
      "mainCaption": "response renamed"
    },
    // deletes response by specifying the id field and sets the isDeleted field
    {
      "id": 68,
      "isDeleted": true
    },
  ]
}
Response output

{
    "id":22,
    "type":1,
    "controlId":31,
    "controlProperties":{
       "controlAlign":"left",
       ...andTheOtherControlProperties
    },
    "responses":[
       {
          "id": 67,
          "mainCaption":"response renamed",
          ...andTheOtherResponseProperties
       },
       {
         "id": 69,
         "mainCaption": "other",
          ...andTheOtherResponseProperties
       }
    ],
    ...andTheOtherQuestionProperties
}
