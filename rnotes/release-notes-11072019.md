# Changes
This section describes all changes in terms of feature development

## Routing validation
When routing creation fails, a default routing is not created anymore.

## Error messages
The list of error messages has been redefined.

## Routings in test mode
When using a test link routings are now working

## Import parameters
Import parameters can now be set on Questions during creation (POST)


## Loops with no Responses
Loops with no responses are now correctly displayed in preview


## Default Language
The question caption is now displayed in preview and test mode when changing the default language of a survey

## Final pages
Final pages can now be set on Survey during creation (POST)

# Known blocking issues

## Default Language
 When changing the default language of the survey the question captions are no longer displayed on live surveys.


## Phantom bug
Responses disappear randomly.


## Modification on questions
Updating a question returns 400 on the API but the changes actually happen.
