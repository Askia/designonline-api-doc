# Routings (survey logic)

This guide is assuming you have at least some experience with interacting with a REST api and that you already had a look at the [Authentification section of this document](intro-authentification.md)

This guide will start right where the other one on [Creating a survey](guide-create-survey.md) ends.
If you did not follow this guide, you'll need to create a survey, add 3 single answer questions and at least two responses to the first question.

In our example first question (q1_gender) is asking respondent about their gender and the available responses are "Man" and "Woman".
Second question (q2_female) is a random question that we will only ask to women. Last question (q3_male) is a question for men only.

Of course if you try to go through the test survey at the end of the previous guide, you'll notice that all questions are being asked no matter if you are a man or woman. This is exactly what survey logic that we call routing is about. Being able to navigate through a survey based on real time context.

In a nutshell a routing is composed of 3 entities:
- The triggering event (the starting point of any routing)
- The condition
- The action

In our example what we'd like to achieve (with routings) can be described in plain english:

```
Rule1: If respondent answers man to q1_gender then route to q3_man
Rule2: If respondent answers woman to q1_gender then route to q2_woman
```

**Our rules both need to get triggered when someone is answering to q1_gender hence the `triggering event`.
Testing if the result is `man` or `woman` is the condition while routing to q3 or q2 is the `action` of the routing.**

These two "rules" do imply a third implicit one. The question are sorted from q1 to q3. Because of that the second rule is not good enough.

Let's go through them:
```
q1_gender -> Man is selected -> Rule 1 is applied -> we are redirected to q3_man -> Survey is finished after that (as this is last question)

q1_gender -> Woman is selected -> Rule 2 is applied -> we are redirected to q2_woman -> Survey continues to q3_man (as this is last question)
```

Obviously after q2_woman we need to exit the survey and there are several ways to achieve that with routings. You can either add a third rule that will trigger on q2_woman and redirect the respondent to the end of the survey or you can alter your rules to have a much nicer "algorithm" to achieve the same result.

Consider these rules:

```
Rule1 bis: Route to q3_male ONLY IF the response of q1_gender is man
Rule2 bis: Route to q2_female ONLY IF the response of q1_gender is woman
```

Even if they are very close to the previous ones they have a subtle change that make the whole thing work.
Now if after q2_female the survey displays q3_male it explicitly violates Rule1 bis.

```
q1_gender -> Man is selected -> Rule 1 is applied -> we are redirected to q3_man -> Survey is finished after that (as this is last question)

q1_gender -> Woman is selected -> Rule 2 is applied -> we are redirected to q2_woman -> Survey CANNOT continue to q3_man (as this violates Rule1 bis) and we are redirected to the exit.
```

## Triggering, Conditions and Actions

In practice you can choose from a variety of triggering events, conditions and actions when using the Design Online API.

To set the triggering right you'll have to provide the Routings endpoints with:

 - The `StartQuestionId`

 - A `StartType`. One of the followings:
 	- Question
  	- All Questions
  	- Start interview
  	- Restart Interview
  	- End Interview

 - An execution event (represented by booleans in the API) that can be either
  	- isAfter
  	- isBefore
  	- isDuring
  	- isEdits
  	- isRunIfNotAsked

To set a condition you'll have to provide a `ConditionType` which should almost have the value of `1` for "Advanced". The `ConditionType` informs the server about how the condition should be interpreted. As we are creating Routings through the API and not trough DesignOnline Software we need it to be set to Advanced and use [AskiaScript](www.askia.com) to describe our execution condition.

The condition itself will be held in the `Condition` field.

The action resides in the `ActionType` field and it's value has to be set to depending of your rules. In our examples we use the `Ask` type which stands for "Only Ask target question if the condition is met", therefore `ActionType = 1`.

Finally you should provide a `targets` object to the API containing the `questionId` to which you want your user to be redirected if the condition is met.  

For a complete description of all the fields have a look at our [API reference](https://www.askia.com)).

Finally to create the Routings you need to call :
`POST {{url}}/AskiaPortal/Modules/design/api/surveys/{{surveyId}}/routings`

the json payloads for both routings can be concatenated inside an array:

```
[
  {
	"name":"Rule1",
	"position":0,
	"startQuestionId":1,
	"startType":0,
	"condition":"((gender Has {1}))",
	"conditionType":1,
	"actionType":1,
	"isAfter":true,
	"isRunIfNotAsked": true,
	"targets":{"questionId":3}
  },
  {
  "name":"Rule2",
  "position":0,
  "startQuestionId":1,
  "startType":0,
  "condition":"((gender Has {2}))",
  "conditionType":1,
  "actionType":1,
  "isAfter":true,
  "isRunIfNotAsked": true,
  "targets":{"questionId":2}
  }
]
```

Note that `((gender Has {1}))` is a piece of code in [AskiaScript](www.askia.com) that describes the condition (that is "If gender has a reponseId of 1")

There are two differences between these two routings described as JSON:
- the condition scripts are not the same as first rule should be triggered when answering **man** to the gender question and the other one **woman**.
- the targets are different as we want redirections to different questions in the survey based on the answer to the gender question

Making the POST request will create both of routings and attach them to your survey.

The cURL command for the routings creation:

```shell
curl -X POST \
  'http://{{url}}/AskiaPortal/Modules/design/api/surveys/{{surveyId}}/routings' \
  -H 'Content-Type: application/json' \
  -H 'Postman-Token: 58686a80-3ce7-414e-9322-d0e4bc6b717b' \
  -H 'cache-control: no-cache' \
  -H 'cookie: {whatever_cookie_value_you_have}' \
  -d '[
  {
	"name":"Routing_from_postman_2",
	"position":0,
	"startQuestionId":1,
	"startType":0,
	"condition":"((gender Has {1}))",
	"conditionType":1,
	"actionType":1,
	"isAfter":true,
	"isRunIfNotAsked": true,
	"targets":{"questionId":3}
  },
  {
  "name":"Rule2",
  "position":0,
  "startQuestionId":1,
  "startType":0,
  "condition":"((gender Has {2}))",
  "conditionType":1,
  "actionType":1,
  "isAfter":true,
  "isRunIfNotAsked": true,
  "targets":{"questionId":2}
  }
]'
```
