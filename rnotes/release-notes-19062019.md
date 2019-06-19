# Changes
This section describes all changes in terms of feature development

## Authentication
A new AskiaPortal Authentication mechanism has been implemented and should be used instead of the previous cookie hack when calling the API routes.

The be fully authenticated you'll need two things:
- An apiKey which is a unique identifier for a registered APP. For now we will provide apiKeys if needed.
- A user session token

Both of them should be passed to requests you make to the API.

To create a user session token call the following endpoint:

`POST {{url}}/AskiaPortal/Modules/design/api/Session?apikey={{your_api_key}}``

This call will authenticate a specific user to the system and grant it with access to the whole API.
The body should be :

```
{
  "username": "your_username",
  "password": "your_password"
}
```

This call will return a session token for this user.

From this point any further authenticated call should include the apiKey as a query string as in:
`POST {{url}}/AskiaPortal/Modules/design/api/Surveys/New?apikey={your_api_key}`

AND the session token in the `askiaportal-session` HTTP header.


## Survey test links
The survey test links are now public (you won't need to be authenticated in AskiaPortal to use them).
The test link format has changed:

```
{{url}}/AskiaPortal/modules/design/api/testex/survey/{{surveyId}}?surveyType={{surveyType}}&action=StartSurvey&interviewSeed={{interviewseed}}}&hash={{the_SALTED_hash_for_this_link}}
```

The hash to provide is essentiel for us to be able to display the survey in test mode. We will provide you with the hash mechanism on demand.


# Known blocking issues

## Publish api
We are still hardly working on the publish API and a new release will soon be available.

## Error messages
We are working on a way to let users define basic and localized error messages on surveys
