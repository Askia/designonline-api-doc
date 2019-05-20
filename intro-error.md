# Errors and error handling

Design Online API uses conventional HTTP response codes to indicate the success or failure of an API request.
Codes in the 2xx range indicate success. Codes in the 4xx range indicate an error that failed given the information provided within the request. Codes in the 5xx range indicate a server internal error.

Application Error responses are enriched with some useful information (in JSON) for clients in order to let them implement fallbacks.


```json
This is an example of the

{
    "message": "The name of the survey demoSurvey already exists.",
    "code": 4070,
    "key": "SurveyNameAlreadyExist",
    "defaultMessage": "The name of the survey `ipsoscallJSON` already exists."
}
```

- **message** : The human readable message addressed to developers or users (depending on the error) localized in whatever language your configured the platform (see Languages & Messages API)

- **code** : an internal code for the error. In general you should not rely on this.
- **key** : The key of the error
- **defaultMessage** : the default message of the error regardless of the choosen language for the platform


# Exhaustive list of error keys and description

## AskiaPortal errors
In addition to DesignOnline API specific errors (see below), you may also receive some platform specific errors. Listed here: [AskiaPortal errors](http://installers.askia.com/HelpDesk/devs/AskiaPortalCmnDoc/html/T_AskiaPortalCmn_Exceptions_ExceptionCode.htm)


## Global errors

  - ItemNotFound: Unable to find the entity in the Askia Design database.
  - NoError: No error.
  - Unspecified: Unspecified error.
  - Unknown: Unknown error.


## Survey related errors

  - UnableToGenerateSurveyFromSurveyTemplate:  Unable to create a survey from a survey template.
  - UnableToCreateSurveyFromAskiaCore: Unable to create the survey in AskiaCore.
  - UnableToSaveSurveyInDesignDatabase: Unable to save the survey in the Askia Design database.
  - UnableChangeSurveyDefaultPageTemplateId:  Unable to change the survey DefaultPageTemplateId
  - UnableToDeserialiseSurveyInput: The input string could not be converted to a SurveyDto.
  - UnableToSetSurveyName: Unable to set the survey `Name`.
  - UnableToSetSurveyDefaultLanguageId: Unable to set the survey `DefaultLanguageId`.
  - UnableToSetSurveyDefaultPageTemplateId: Unable to set the survey `DefaultPageTemplateId`.
  - UnableToSetSurveyPageTemplateProperties: Unable to set the survey `PageTemplateProperties`.
  - UnableToSetSurveyThemeProperties: Unable to set the survey `ThemeProperties`.
  - SurveyExtractResourcesFailure: The resources for the survey could not be extracted.
  - SurveyNoFileInRequest: The HTTP request is required to contain a file but none was found.
  - SurveyLanguageTextsFileEmptyInRequest: The HTTP request is required to contain a file. The file is present but is empty.
  - SurveyLanguageTextsFileNotReadable: An error occured while trying to access the file stream for the survey language texts
  - UnableToCreateSubSurveyFromQuestion: An error occurred when trying to create a sub-survey based on a question in the existing survey.
  - SurveyMoveRoutingsFailure: Unable to move the routings.
  - UnableToSaveRoutingsInDesignDatabase: Unable to save the routings.


## Scenario related errors


  - UnableToSaveScenarioInDesignDatabase: Unable to save the scenario in the Askia Design database.
  - UnableToCreateScenarioFromAskiaCore: Unable to create the scenario in AskiaCore.
  - UnableToDeleteScenarioFromAskiaCore: Unable to delete the scenario in AskiaCore.
  - UnableToSetScenarioName: Unable to set the scenario `Name`.
  - ScenarioNameInvalid: AskiaCore rejected the supplied scenario name.
  - ScenarioNameNotUnique: AskiaCore rejected the supplied scenario name as non-unique.


## ScenarioEntity related errors

  - UnknownScenarioEntityType: Unknown scenario entity type.
  - UnableToCreateScenarioEntityFromAskiaCore: Unable to create the scenario entity in AskiaCore.
  - UnableToSaveScenarioEntityFromAskiaCore: Unable to create the scenario entity in AskiaCore.
  - UnallowedToUpdateScenarioEntityFromAskiaCore: Unable to update the scenario entity in AskiaCore.
  - UnableToDeleteScenarioEntityFromAskiaCore: Unable to delete the scenario entity in AskiaCore.



## Question related errors

  - QuestionNotFoundInDesignDatabase: Unable to find the question in the Askia Design database.
  - UnableToDeleteQuestionFromAskiaCore: Unable to delete the question in AskiaCore.
  - QuestionPrevSiblingIdValueSet: Question.PrevSiblingId was assigned a value instead of null.
  This property cannot be set explicitly.
  - QuestionPositionValueSet: Question.Position was assigned a value instead of null.
  This property cannot be set explicitly.
  - QuestionIsFirstInPageValueSet: Question.IsFirstInPage was assigned a value instead of null.
  This property cannot be set explicitly.
  - QuestionIsLastInPageValueSet: Question.IsLastInPage was assigned a value instead of null.
  This property cannot be set explicitly.
  - QuestionMergingPageIdValueSet: Question.MergingPageId was assigned a value instead of null.
  This property cannot be set explicitly.
  - UnableToCreateQuestionFromAskiaCore: Unable to create the scenario in AskiaCore.
  - QuestionRestoreFailureNotFound: The question to restore could not be found using the supplied question ID.
  - QuestionRestoreFailureNotDeleted: The question to restore is already not marked as deleted.
  - QuestionInvalidImpTypeValue: The question ImpType value is invalid.
  - QuestionInvalidImpClosedMatchingTypeValue: The question ImpClosedMatchingType value is invalid.
  - QuestionInvalidImpPanelUpdateTypeValue: The question ImpPanelUpdateType value is invalid.
  - QuestionInvalidLinkTypeValue: The question LinkType value is invalid.
  - QuestionInvalidRotationTypeValue: The question RotationType value is invalid.
  - QuestionInvalidVisibilityValue: The question Visibility value is invalid.
  - QuestionInvalidShortcutValue: The question Shortcut value is invalid.
  - QuestionInvalidTypeValue: The question Type value is invalid.
  - QuestionSetExtensionFailure: The question control element control could not be set.
  - UnableToSaveQuestionInDesignDatabase: Unable to save the question in the Askia Design database.
  - UnableToSaveResponsesInDesignDatabase: Unable to save the list of responses in the Askia Design database.
  - QuestionInvalidIdValue: The question Id value is invalid.
  - QuestionNextSiblingIdNotFound: No question with an ID equal to the NextSiblingId value could be found.
  - QuestionMovementParentIdPrevSiblingMismatch: The supplied parent question is not the parent for the supplied previous sibling question.
  - QuestionMovementFailure: The questions could not be moved. AskiaCore returned an error.
  - QuestionMovementSaveFailure: An error occurred saving the survey after moving the questions.
  - QuestionIndentFailure: The questions could not be indented. AskiaCore returned an error.
  - QuestionIndentSaveFailure: An error occurred saving the survey after indenting the questions.
  - QuestionUnindentFailure: The questions could not be unindented. AskiaCore returned an error.
  - QuestionUnindentSaveFailure: An error occurred saving the survey after unindenting the questions.
  - QuestionSplitFailure: The questions could not be split. AskiaCore returned an error.
  - QuestionSplitSaveFailure: An error occurred saving the survey after splitting the questions.
  - QuestionMergeFailure: The questions could not be merged. AskiaCore returned an error.
  - QuestionMergeSaveFailure: An error occurred saving the survey after merging the questions.
  - QuestionTypeNullOrInvalid: The question type was null or invalid.
  - QuestionLinkTypeNullOrInvalid: The question link type was null or invalid.
  - QuestionRotationTypeNullOrInvalid: The question rotation type was null or invalid.
  - QuestionAnonymisationTypeNullOrInvalid: The question anonymisation type was null or invalid.

## Question related errors

  - ElementSaveFailure: The question control element could not be saved.
  - UnableToCreateElementFromAskiaCore: Unable to create the element in AskiaCore.
  - ElementControlNotFound: Unable to find the control associated to the element.
  - ElementPageTemplateNotFound: Unable to find the page template associated to the element.
  - ElementPrevSiblingIdValueSet: Element.PrevSiblingId was assigned a value instead of null.
	This property cannot be set explicitly.
  - ElementPositionValueSet: Element.Position was assigned a value instead of null.
  This property cannot be set explicitly.
  - ElementInvalidTypeValue: The element Type value is invalid.
  - ElementNextSiblingNotFound: The element targeted as the next sibling could not be found by the ID supplied.
  - UnableToSaveElementInDesignDatabase: Unable to save the element in the Askia Design database.
  - UnableToDeleteElementFromAskiaCore: Unable to delete the element in the Askia Design database.
  - UnableToMoveElementInAskiaCore: Unable to move the element in the Askia Design database.
  - ElementPrevSiblingNotFound: Unable to find sibling element in the Askia Design database.
  - ElementMovementParentIdPrevSiblingMismatch: The supplied parent element is not the parent for the supplied previous sibling element.
  - ElementFirstChildIdValueSet: Element.FirstChildId was assigned a value instead of null.
	This property cannot be set explicitly.
  - ElementIsDeletedValueSet: Element.IsDeleted was assigned a value instead of null.
	This property cannot be set explicitly.
  - ElementLastChildIdValueSet: Element.LastChildId was assigned a value instead of null.
	This property cannot be set explicitly.
  - ElementNextSiblingIdValueSet: Element.NextSiblingId was assigned a value instead of null.
	This property cannot be set explicitly.
  - ElementParentIdValueSet: Element.ParentId was assigned a value instead of null.
	This property cannot be set explicitly.
  - ElementQuestionIdValueSet: Element.QuestionId was assigned a value instead of null.
	This property cannot be set explicitly.
  - ElementSeedValueSet: Element.Seed was assigned a value instead of null.
	This property should not be set explicitly for this operation.


## Response related errors

  - ResponseNotFoundInDesignDatabase: Unable to find the response in the Askia Design database.
  - ResponseInvalidIdValue: The response Id value is invalid.
  - ResponsePositionValueSet: Response.Position was assigned a value instead of null.
	This property cannot be set explicitly.
  - ResponseNextSiblingIdNotFound: No response with an ID equal to the NextSiblingId value could be found.
  - ResponsePrevSiblingIdNotFound: No response with an ID equal to the PrevSiblingId value could be found.
  - UnableToSaveResponseInDesignDatabase: Unable to save the response in the Askia Design database.
  - UnableToDeleteResponseFromAskiaCore: Unable to delete the response in AskiaCore.
  - UnableToCreateResponseFromAskiaCore: Unable to create the response in AskiaCore.
  - UnableToCreateResponsesFromAskiaCore: Unable to create the responses in AskiaCore.
  - ResponseQuestionIdInvalidValueSet: The questionID value in the response DTO does not match the ID
	of the question that the response is to be added to.
  - ResponseInvalidTypeValue: The response Type value is invalid.
  - ResponseInvalidBaseTypeValue: The response BaseType value is invalid.
  - ResponseInvalidRotationBehaviourValue: The response RotationBehaviour value is invalid.
  - ResponseMovementParentIdPrevSiblingMismatch: The supplied parent response is not the parent for the supplied
	previous sibling response.
  - ResponseMovementFailure: The responses could not be moved. AskiaCore returned an error.
  - ResponsesIndentFailure: The responses could not be indented. AskiaCore returned an error.
  - ResponsesIndentSaveFailure: An error occurred saving the survey after indenting the responses.
  - ResponsesUnindentFailure: The responses could not be unindented. AskiaCore returned an error.
  - ResponsesUnindentSaveFailure: An error occurred saving the survey after unindenting the responses.
  - ResponseMovementSaveFailure: An error occurred saving the survey after moving the responses.
  - ResponseIndentSaveFailure: An error occurred saving the survey after indenting the responses.
  - ResponseUnindentSaveFailure: An error occurred saving the survey after unindenting the responses.
  - ResponseTypeNullOrInvalid: The response type was null or invalid.
  - ResponseBaseTypeNullOrInvalid: The response base type was null or invalid.
  - ResponseRotationBehaviourNullOrInvalid: The response rotation behaviour type was null or invalid.

## ResponseLink related errors

  - UnableToSaveResponseLinkInDesignDatabase:
  - UnableToCreateResponseLinkFromAskiaCore: Unable to create the linked response in AskiaCore.
  - UnableToDeleteResponseLinkFromAskiaCore:


## Routings related errors  

  - UnableToCreateRoutingFromAskiaCore: Unable to create the routing in AskiaCore.
  - UnableToSaveRoutingInDesignDatabase: Unable to save the routing in the Askia Design database.
  - UnableToPositionRoutingInDesignDatabase: Unable to position the routing in the Askia Design database.
  - UnableToDeleteRoutingFromAskiaCore: Unable to delete the routing in AskiaCore.
  - RoutingNullActionType: The supplied routing action type value is 'null' when a value is required.
  - RoutingInvalidActionType: The supplied routing action type value is not a valid or recognised.
  - RoutingActionTypeNullOrInvalid: The routing action type was null or invalid.
  - RoutingConditionTypeNullOrInvalid: The routing condition type was null or invalid.
  - RoutingConditionInvalid: The routing condition could not be set. AskiaCore rejected it.
  - RoutingNotFoundInDesignDatabase: Unable to find the routing in the Askia Design database.
  - RoutingIsDeletedValueSet: Routing.IsDeleted was assigned a value instead of null.
	This property cannot be set explicitly.
  - RoutingCaptionInvalidType: The supplied routing caption type value is not a valid or recognised.
  - RoutingCaptionInvalid: The supplied routing caption type is not valid for the action of this routing.
  - UnableToDeleteRoutingTargetsFromAskiaCore: Unable to delete the routing targets for a routing in AskiaCore.
  - RoutingInvalidActionParameterValue: Unable to set the action parameter value for a routing in AskiaCore.
  - RoutingStartQuestionIdNotSet: Unable to create a routing without the start question ID.
  - RoutingIdNotSet: The ID of the routing is required but missing.
  - RoutingIdsNotSet: The IDs of the routings are required but missing.
  - RoutingPositionNotSet: The target position of the routing(s) was not set.
  - RoutingStartQuestionNotSet: The start question of the routing(s) was not set.
  - RoutingStartTypeNotSet: The start type of the routing(s) was not set.
  - RoutingStartQuestionNotFound: The start question for the routing could not be found using the supplied identifier.
  - RoutingUnableToGetAffectedEntities: AskiaCore was unable to identify the entities affected by the operation.
  - RoutingNameRejected: AskiaCore rejected the supplied routing name.
  - RoutingStartTypeNullOrInvalid: The routing start type was null or invalid.


## RoutingTarget related errors

  - RoutingTargetInvalidType: The supplied routing target type value is not a valid or recognised.
  - UnableToCreateRoutingTargetFromAskiaCore: Unable to create the scenario in AskiaCore.
  - UnableToSaveRoutingTargetInDesignDatabase: Unable to save the routing target in the Askia Design database.
  - UnableToDeleteRoutingTargetFromAskiaCore: Unable to delete the routing target in AskiaCore.
  - ResponseTargetIdInvalidValue: The response target ID value supplied is not valid.
  - ResponseTargetTypeInvalidValue: The response target type value supplied is not valid.
  - ResponseTargetNullQuestionIdValue: The response target type value supplied is null.



## HtmlRendering related errors

  - HtmlRenderIsNull: Null value returned from PageElement.RenderPage().
  - HtmlRenderErrorsOccurred: The page could not be rendered. AskiaCore returned errors.


## Test Survey related errors

  - InvalidSurveyAction: The supplied action for testing a survey is not valid.
  - UnableToSaveInterview: The interview for the survey testing could not be saved.
  - UnableToLoadInterview: The interview for the survey testing could not be loaded.
  - UnableToRenderInterviewPage: The current page of the survey interview could not be rendered.
  - InvalidInterviewAction: The interview action was empty or invalid.
  - UnableToMoveWithinFinishedInterview: The interview is marked as finished and the user attempted to move to a different screen, which is not permitted.
  - NullValueWhenMovingWithinInterviewInAskiaCore: AskiaCore returned an empty value when attempting to move the interview to a different screen.
  - ErrorWhenMovingWithinInterviewInAskiaCore: AskiaCore returned an error when attempting to move the interview to a different screen.
  - ExceptionWhenMovingWithinInterview: An exception occurred when attempting to move an interview to a different screen.


## Resource related errors

  - ResourceNotFoundInDesignDatabase: Unable to find the resource in the Askia Design database.
  - ResourcesNoFileInRequest: The HTTP request to create a resource did not contain the required resource file.
  - ResourceFileEmptyInRequest: The HTTP request resource file was empty.
  - ResourceFileNameAlreadyInUse: Could not create a resource because a file with same name already exists.
  - ResourceUploadFileNotReadable: An error occured while trying to access the file stream for a resource.
  - ResourceSaveFailure: Unable to save the resource in the Askia Design database.
  - ResourceFileDescriptorsNotFoundOrInvalid: The required resource files descriptors were not found or were invalid.
  - UnableToDeleteResourceFromAskiaCore: Unable to delete the resource in AskiaCore.
  - ResourceTypeNullOrInvalid: The resource type was null or invalid.
  - UnableToCreateResourceFromAskiaCore: Unable to create the resource in AskiaCore.


## Languages related errors

  - UnrecognisedLanguageIds: At least one of the language IDs supplied is not recognised.
  - UnableToParseLanguageIds: The list of language IDs could not be parsed. It should be a comma-delimited string.


## SurveyLanguages related errors

  - UnableToCreateSurveyLanguageFromAskiaCore: Unable to create the survey language in AskiaCore.
  - SurveyTextsFileNotFoundOrInvalid: The required survey texts CSV file was not found or was invalid.
  - SurveyTextsFileCouldNotBeRead: The required survey texts CSV file was provided but could not be read.


## PublishSurvey related errors  


  - CcaWebServerNotFound: The CcaWebServer could not be found or is not accessible to the user.
  - ItemDoesntExist: The item could not be found or is not accessible to the user.


## User related errors

  - UserNotFoundInPortal: The user could not be found in AskiaPortal.


## Misc errors

  - ItemsEmptyArray: No item IDs were supplied.
  - ItemsInsufficientArray: Insufficient item IDs were supplied.
  - UnableToDeserialiseJsonInput: The input string could not be converted to a dto.
  - UnableToSerialiseToJson: The dto could not be serialised to a Json string.
  - InputIsNull: No input was supplied.
  - InvalidQuestionTypeForDefaultControlValue: The supplied value could not be converted into a question type for default control.
