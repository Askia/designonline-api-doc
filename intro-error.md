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

- **message** : The human readable message addressed to developers or users (depending on the error) localized in whatever language your configured the plateform (see Languages & Messages API)

- **code** : an internal code for the error. In general you should not rely on this.
- **key** : The key of the error
- **defaultMessage** : the default message of the error regardless of the choosen language for the platform


## Application error list

  ItemNotFound: Unable to find the entity in the Askia Design database.,

  UnableToGenerateSurveyFromSurveyTemplate:  Unable to create a survey from a survey template.

  UnableToCreateSurveyFromAskiaCore: Unable to create the survey in AskiaCore.


        /// <summary>
        ///   Unable to a survey with the AskiaCore.
        ///   (Code: 50002)
        /// </summary>
        UnableToDeleteSurveyFromAskiaCore,

        /// <summary>
        ///   Unable to save the survey in the Askia Design database.
        /// </summary>
        UnableToSaveSurveyInDesignDatabase,

        /// <summary>
        ///   Unable to change the survey DefaultPageTemplateId .
        /// </summary>
        UnableChangeSurveyDefaultPageTemplateId,

	    /// <summary>
	    /// The input string could not be converted to a SurveyDto.
	    /// </summary>
	    UnableToDeserialiseSurveyInput,

	    /// <summary>
	    ///   Unable to set the survey `Name`.
	    /// </summary>
	    UnableToSetSurveyName,

		/// <summary>
		///   Unable to set the survey `DefaultLanguageId`.
		/// </summary>
	    UnableToSetSurveyDefaultLanguageId,

		/// <summary>
		///   Unable to set the survey `DefaultPageTemplateId`.
		/// </summary>
		UnableToSetSurveyDefaultPageTemplateId,

	    /// <summary>
	    ///   Unable to set the survey `PageTemplateProperties`.
	    /// </summary>
	    UnableToSetSurveyPageTemplateProperties,

	    /// <summary>
	    ///   Unable to set the survey `ThemeProperties`.
	    /// </summary>
	    UnableToSetSurveyThemeProperties,

	    /// <summary>
	    /// The resources for the survey could not be extracted.
	    /// </summary>
	    SurveyExtractResourcesFailure,

		/// <summary>
		/// The HTTP request is required to contain a file but none was found.
		/// </summary>
		SurveyNoFileInRequest,

	    /// <summary>
	    /// The HTTP request is required to contain a file. The file is present but is empty.
	    /// </summary>
	    SurveyLanguageTextsFileEmptyInRequest,


		/// <summary>
		/// An error occured while trying to access the file stream for the survey language texts.
		/// </summary>
		SurveyLanguageTextsFileNotReadable,

		/// <summary>
		/// An error occurred when trying to create a sub-survey based on a question in the existing survey.
		/// </summary>
	    UnableToCreateSubSurveyFromQuestion,

		/// <summary>
		/// Unable to move the routings.
		/// </summary>
		SurveyMoveRoutingsFailure,

		/// <summary>
		/// Unable to save the routings.
		/// </summary>
		UnableToSaveRoutingsInDesignDatabase,
		#endregion

		#region Scenario
		/// <summary>
		///   Unable to save the scenario in the Askia Design database.
		/// </summary>
		UnableToSaveScenarioInDesignDatabase,

	    /// <summary>
	    ///   Unable to create the scenario in AskiaCore.
	    /// </summary>
	    UnableToCreateScenarioFromAskiaCore,

	    /// <summary>
	    ///   Unable to delete the scenario in AskiaCore.
	    /// </summary>
	    UnableToDeleteScenarioFromAskiaCore,

	    /// <summary>
	    ///   Unable to set the scenario `Name`.
	    /// </summary>
	    UnableToSetScenarioName,

		/// <summary>
		/// AskiaCore rejected the supplied scenario name.
		/// </summary>
		ScenarioNameInvalid,
		/// <summary>
		/// AskiaCore rejected the supplied scenario name as non-unique.
		/// </summary>
		ScenarioNameNotUnique,
	    #endregion

		#region ScenarioEntity
		/// <summary>
		///   Unknow scenario entity type.
		/// </summary>
		UnknownScenarioEntityType,

	    /// <summary>
	    ///   Unable to create the scenario entity in AskiaCore.
	    /// </summary>
	    UnableToCreateScenarioEntityFromAskiaCore,

	    /// <summary>
	    ///   Unable to create the scenario entity in AskiaCore.
	    /// </summary>
	    UnableToSaveScenarioEntityFromAskiaCore,

	    /// <summary>
	    ///   Unable to delete the scenario entity in AskiaCore.
	    /// </summary>
	    UnallowedToUpdateScenarioEntityFromAskiaCore,

	    /// <summary>
	    ///   Unable to delete the scenario entity in AskiaCore.
	    /// </summary>
	    UnableToDeleteScenarioEntityFromAskiaCore,
	    #endregion

	    #region Question
		/// <summary>
		/// Unable to find the question in the Askia Design database.
		/// </summary>
		QuestionNotFoundInDesignDatabase,

		/// <summary>
		/// Unable to delete the question in AskiaCore.
		/// </summary>
	    UnableToDeleteQuestionFromAskiaCore,

        /// <summary>
        /// Question.PrevSiblingId was assigned a value instead of null.
        /// This property cannot be set explicitly.
        /// </summary>
        QuestionPrevSiblingIdValueSet,

        /// <summary>
        /// Question.Position was assigned a value instead of null.
        /// This property cannot be set explicitly.
        /// </summary>
        QuestionPositionValueSet,

        /// <summary>
        /// Question.IsFirstInPage was assigned a value instead of null.
        /// This property cannot be set explicitly.
        /// </summary>
        QuestionIsFirstInPageValueSet,

        /// <summary>
        /// Question.IsLastInPage was assigned a value instead of null.
        /// This property cannot be set explicitly.
        /// </summary>
        QuestionIsLastInPageValueSet,

        /// <summary>
        /// Question.MergingPageId was assigned a value instead of null.
        /// This property cannot be set explicitly.
        /// </summary>
        QuestionMergingPageIdValueSet,

	    /// <summary>
	    ///   Unable to create the scenario in AskiaCore.
	    ///   (Code: 60007)
	    /// </summary>
        UnableToCreateQuestionFromAskiaCore,

		/// <summary>
		/// The question to restore could not be found using the supplied question ID.
		/// </summary>
		QuestionRestoreFailureNotFound,

	    /// <summary>
	    /// The question to restore is already not marked as deleted.
	    /// </summary>
	    QuestionRestoreFailureNotDeleted,

		/// <summary>
		/// The question ImpType value is invalid.
		/// </summary>
		QuestionInvalidImpTypeValue,

		/// <summary>
		/// The question ImpClosedMatchingType value is invalid.
		/// </summary>
		QuestionInvalidImpClosedMatchingTypeValue,

		/// <summary>
		/// The question ImpPanelUpdateType value is invalid.
		/// </summary>
		QuestionInvalidImpPanelUpdateTypeValue,

		/// <summary>
		/// The question LinkType value is invalid.
		/// </summary>
		QuestionInvalidLinkTypeValue,

	    /// <summary>
	    /// The question RotationType value is invalid.
	    /// </summary>
	    QuestionInvalidRotationTypeValue,

	    /// <summary>
	    /// The question Visibility value is invalid.
	    /// </summary>
	    QuestionInvalidVisibilityValue,

		/// <summary>
		/// The question Shortcut value is invalid.
		/// </summary>
		QuestionInvalidShortcutValue,

	    /// <summary>
	    /// The question Type value is invalid.
	    /// </summary>
	    QuestionInvalidTypeValue,

	    /// <summary>
	    /// The question control element control could not be set.
	    /// </summary>
	    QuestionSetExtensionFailure,

	    /// <summary>
	    ///   Unable to save the question in the Askia Design database.
	    /// </summary>
	    UnableToSaveQuestionInDesignDatabase,

	    /// <summary>
	    ///   Unable to save the list of responses in the Askia Design database.
	    /// </summary>
	    UnableToSaveResponsesInDesignDatabase,

		/// <summary>
		/// The question Id value is invalid.
		/// </summary>
		QuestionInvalidIdValue,

		/// <summary>
		/// No question with an ID equal to the NextSiblingId value could be found.
		/// </summary>
		QuestionNextSiblingIdNotFound,

	    /// <summary>
	    /// The supplied parent question is not the parent for the supplied previous sibling question.
	    /// </summary>
	    QuestionMovementParentIdPrevSiblingMismatch,

		/// <summary>
		/// The questions could not be moved. AskiaCore returned an error.
		/// </summary>
		QuestionMovementFailure,

		/// <summary>
		/// An error occurred saving the survey after moving the questions.
		/// </summary>
		QuestionMovementSaveFailure,

	    /// <summary>
	    /// The questions could not be indented. AskiaCore returned an error.
	    /// </summary>
	    QuestionIndentFailure,

		/// <summary>
		/// An error occurred saving the survey after indenting the questions.
		/// </summary>
		QuestionIndentSaveFailure,

	    /// <summary>
	    /// The questions could not be unindented. AskiaCore returned an error.
	    /// </summary>
	    QuestionUnindentFailure,

	    /// <summary>
	    /// An error occurred saving the survey after unindenting the questions.
	    /// </summary>
	    QuestionUnindentSaveFailure,

	    /// <summary>
	    /// The questions could not be split. AskiaCore returned an error.
	    /// </summary>
	    QuestionSplitFailure,

		/// <summary>
		/// An error occurred saving the survey after splitting the questions.
		/// </summary>
		QuestionSplitSaveFailure,

	    /// <summary>
	    /// The questions could not be merged. AskiaCore returned an error.
	    /// </summary>
	    QuestionMergeFailure,

	    /// <summary>
	    /// An error occurred saving the survey after merging the questions.
	    /// </summary>
	    QuestionMergeSaveFailure,

	    /// <summary>
	    /// The question type was null or invalid.
	    /// </summary>
	    QuestionTypeNullOrInvalid,

		/// <summary>
		/// The question link type was null or invalid.
		/// </summary>
	    QuestionLinkTypeNullOrInvalid,

		/// <summary>
		/// The question rotation type was null or invalid.
		/// </summary>
	    QuestionRotationTypeNullOrInvalid,

		/// <summary>
		/// The question anonymisation type was null or invalid.
		/// </summary>
		QuestionAnonymisationTypeNullOrInvalid,
		#endregion

		#region Element
		/// <summary>
		/// The question control element could not be saved.
		/// </summary>
		ElementSaveFailure,

		/// <summary>
		/// Unable to create the element in AskiaCore.
		/// </summary>
	    UnableToCreateElementFromAskiaCore,

		/// <summary>
		/// Unable to find the control associated to the element.
		/// </summary>
	    ElementControlNotFound,

	    /// <summary>
	    /// Unable to find the page template associated to the element.
	    /// </summary>
	    ElementPageTemplateNotFound,

		/// <summary>
		/// Element.PrevSiblingId was assigned a value instead of null.
		/// This property cannot be set explicitly.
		/// </summary>
		ElementPrevSiblingIdValueSet,

		/// <summary>
		/// Element.Position was assigned a value instead of null.
		/// This property cannot be set explicitly.
		/// </summary>
		ElementPositionValueSet,

	    /// <summary>
	    /// The element Type value is invalid.
	    /// </summary>
	    ElementInvalidTypeValue,

		/// <summary>
		/// The element targeted as the next sibling could not be found by the ID supplied.
		/// </summary>
		ElementNextSiblingNotFound,

		/// <summary>
		///   Unable to save the element in the Askia Design database.
		/// </summary>
		UnableToSaveElementInDesignDatabase,

		/// <summary>
		/// Unable to delete the element in the Askia Design database.
		/// </summary>
	    UnableToDeleteElementFromAskiaCore,

	    /// <summary>
	    /// Unable to move the element in the Askia Design database.
	    /// </summary>
	    UnableToMoveElementInAskiaCore,

		/// <summary>
		/// Unable to find sibling element in the Askia Design database.
		/// </summary>
	    ElementPrevSiblingNotFound,

	    /// <summary>
	    /// The supplied parent element is not the parent for the supplied previous sibling element.
	    /// </summary>
	    ElementMovementParentIdPrevSiblingMismatch,

		/// <summary>
		/// Element.FirstChildId was assigned a value instead of null.
		/// This property cannot be set explicitly.
		/// </summary>
		ElementFirstChildIdValueSet,

		/// <summary>
		/// Element.IsDeleted was assigned a value instead of null.
		/// This property cannot be set explicitly.
		/// </summary>
	    ElementIsDeletedValueSet,

		/// <summary>
		/// Element.LastChildId was assigned a value instead of null.
		/// This property cannot be set explicitly.
		/// </summary>
		ElementLastChildIdValueSet,

		/// <summary>
		/// Element.NextSiblingId was assigned a value instead of null.
		/// This property cannot be set explicitly.
		/// </summary>
		ElementNextSiblingIdValueSet,

		/// <summary>
		/// Element.ParentId was assigned a value instead of null.
		/// This property cannot be set explicitly.
		/// </summary>
	    ElementParentIdValueSet,

		/// <summary>
		/// Element.QuestionId was assigned a value instead of null.
		/// This property cannot be set explicitly.
		/// </summary>
		ElementQuestionIdValueSet,

	    /// <summary>
	    /// Element.Seed was assigned a value instead of null.
	    /// This property should not be set explicitly for this operation.
	    /// </summary>
	    ElementSeedValueSet,
		#endregion

		#region Response
		/// <summary>
		/// Unable to find the response in the Askia Design database.
		/// </summary>
		ResponseNotFoundInDesignDatabase,

	    /// <summary>
	    /// The response Id value is invalid.
	    /// </summary>
	    ResponseInvalidIdValue,

		/// <summary>
		/// Response.Position was assigned a value instead of null.
		/// This property cannot be set explicitly.
		/// </summary>
		ResponsePositionValueSet,

		/// <summary>
		/// No response with an ID equal to the NextSiblingId value could be found.
		/// </summary>
		ResponseNextSiblingIdNotFound,

	    /// <summary>
	    /// No response with an ID equal to the PrevSiblingId value could be found.
	    /// </summary>
	    ResponsePrevSiblingIdNotFound,

		/// <summary>
		///   Unable to save the response in the Askia Design database.
		/// </summary>
		UnableToSaveResponseInDesignDatabase,

	    /// <summary>
	    /// Unable to delete the response in AskiaCore.
	    /// </summary>
	    UnableToDeleteResponseFromAskiaCore,

	    /// <summary>
	    ///   Unable to create the response in AskiaCore.
	    /// </summary>
	    UnableToCreateResponseFromAskiaCore,

	    /// <summary>
	    ///   Unable to create the responses in AskiaCore.
	    /// </summary>
	    UnableToCreateResponsesFromAskiaCore,

		/// <summary>
		/// The questionID value in the response DTO does not match the ID
		/// of the question that the response is to be added to.
		/// </summary>
		ResponseQuestionIdInvalidValueSet,

	    /// <summary>
	    /// The response Type value is invalid.
	    /// </summary>
	    ResponseInvalidTypeValue,

		/// <summary>
		/// The response BaseType value is invalid.
		/// </summary>
	    ResponseInvalidBaseTypeValue,

		/// <summary>
		/// The response RotationBehaviour value is invalid.
		/// </summary>
		ResponseInvalidRotationBehaviourValue,

		/// <summary>
		/// The supplied parent response is not the parent for the supplied
		/// previous sibling response.
		/// </summary>
		ResponseMovementParentIdPrevSiblingMismatch,

	    /// <summary>
	    /// The responses could not be moved. AskiaCore returned an error.
	    /// </summary>
	    ResponseMovementFailure,

	    /// <summary>
	    /// The responses could not be indented. AskiaCore returned an error.
	    /// </summary>
	    ResponsesIndentFailure,

		/// <summary>
		/// An error occurred saving the survey after indenting the responses.
		/// </summary>
		ResponsesIndentSaveFailure,

		/// <summary>
		/// The responses could not be unindented. AskiaCore returned an error.
		/// </summary>
		ResponsesUnindentFailure,

		/// <summary>
		/// An error occurred saving the survey after unindenting the responses.
		/// </summary>
		ResponsesUnindentSaveFailure,

	    /// <summary>
	    /// An error occurred saving the survey after moving the responses.
	    /// </summary>
	    ResponseMovementSaveFailure,

	    /// <summary>
	    /// An error occurred saving the survey after indenting the responses.
	    /// </summary>
	    ResponseIndentSaveFailure,

	    /// <summary>
	    /// An error occurred saving the survey after unindenting the responses.
	    /// </summary>
	    ResponseUnindentSaveFailure,

	    /// <summary>
	    /// The response type was null or invalid.
	    /// </summary>
	    ResponseTypeNullOrInvalid,

	    /// <summary>
	    /// The response base type was null or invalid.
	    /// </summary>
	    ResponseBaseTypeNullOrInvalid,

		/// <summary>
		/// The response rotation behaviour type was null or invalid.
		/// </summary>
		ResponseRotationBehaviourNullOrInvalid,
		#endregion

		#region ResponseLink
		/// <summary>
		///
		/// </summary>
		UnableToSaveResponseLinkInDesignDatabase,

	    /// <summary>
	    ///   Unable to create the linked response in AskiaCore.
	    /// </summary>
	    UnableToCreateResponseLinkFromAskiaCore,

	    /// <summary>
	    ///
	    /// </summary>
	    UnableToDeleteResponseLinkFromAskiaCore,
	    #endregion

	    #region HtmlRendering
	    /// <summary>
	    /// Null value returned from PageElement.RenderPage().
	    /// </summary>
	    HtmlRenderIsNull,

	    /// <summary>
	    /// The page could not be rendered. AskiaCore returned errors.
	    /// </summary>
	    HtmlRenderErrorsOccurred,
	    #endregion

	    #region Misc
	    /// <summary>
	    /// No item IDs were supplied.
	    /// </summary>
	    ItemsEmptyArray,

	    /// <summary>
	    /// Insufficient item IDs were supplied.
	    /// </summary>
	    ItemsInsufficientArray,

	    /// <summary>
	    /// The input string could not be converted to a dto.
	    /// </summary>
	    UnableToDeserialiseJsonInput,

	    /// <summary>
	    /// The dto could not be serialised to a Json string.
	    /// </summary>
	    UnableToSerialiseToJson,

		/// <summary>
		/// No input was supplied.
		/// </summary>
		InputIsNull,

		/// <summary>
		/// The supplied value could not be converted into a question type for default control.
		/// </summary>
		InvalidQuestionTypeForDefaultControlValue,
		#endregion

		#region Test Survey
		/// <summary>
		/// The supplied action for testing a survey is not valid.
		/// </summary>
		InvalidSurveyAction,

		/// <summary>
		/// The interview for the survey testing could not be saved.
		/// </summary>
	    UnableToSaveInterview,

	    /// <summary>
	    /// The interview for the survey testing could not be loaded.
	    /// </summary>
		UnableToLoadInterview,

		/// <summary>
		/// The current page of the survey interview could not be rendered.
		/// </summary>
	    UnableToRenderInterviewPage,

		/// <summary>
		/// The interview action was empty or invalid.
		/// </summary>
		InvalidInterviewAction,

		/// <summary>
		/// The interview is marked as finished and the user attempted to move to a different screen, which is not permitted.
		/// </summary>
		UnableToMoveWithinFinishedInterview,

	    /// <summary>
	    /// AskiaCore returned an empty value when attempting to move the interview to a different screen.
	    /// </summary>
	    NullValueWhenMovingWithinInterviewInAskiaCore,

		/// <summary>
		/// AskiaCore returned an error when attempting to move the interview to a different screen.
		/// </summary>
	    ErrorWhenMovingWithinInterviewInAskiaCore,

	    /// <summary>
	    /// An exception occurred when attempting to move an interview to a different screen.
	    /// </summary>
	    ExceptionWhenMovingWithinInterview,
		#endregion

		#region Resource
	    /// <summary>
	    /// Unable to find the resource in the Askia Design database.
	    /// </summary>
	    ResourceNotFoundInDesignDatabase,

		/// <summary>
		/// The HTTP request to create a resource did not contain the required resource file.
		/// </summary>
	    ResourcesNoFileInRequest,

		/// <summary>
		/// The HTTP request resource file was empty.
		/// </summary>
		ResourceFileEmptyInRequest,

		/// <summary>
		/// Could not create a resource because a file with same name already exists.
		/// </summary>
		ResourceFileNameAlreadyInUse,

		/// <summary>
		/// An error occured while trying to access the file stream for a resource.
		/// </summary>
		ResourceUploadFileNotReadable,


		/// <summary>
		///   Unable to save the resource in the Askia Design database.
		/// </summary>
	    ResourceSaveFailure,

		/// <summary>
		/// The required resource files descriptors were not found or were invalid.
		/// </summary>
		ResourceFileDescriptorsNotFoundOrInvalid,

	    /// <summary>
	    ///   Unable to delete the resource in AskiaCore.
	    /// </summary>
	    UnableToDeleteResourceFromAskiaCore,

	    /// <summary>
	    /// The resource type was null or invalid.
	    /// </summary>
	    ResourceTypeNullOrInvalid,

	    /// <summary>
	    ///   Unable to create the resource in AskiaCore.
	    /// </summary>
	    UnableToCreateResourceFromAskiaCore,
		#endregion

		#region Languages
		/// <summary>
		/// At least one of the language IDs supplied is not recognised.
		/// </summary>
		UnrecognisedLanguageIds,

	    /// <summary>
	    /// The list of language IDs could not be parsed. It should be a comma-delimited string.
	    /// </summary>
	    UnableToParseLanguageIds,
		#endregion

		#region SurveyLanguages
		/// <summary>
		/// Unable to create the survey language in AskiaCore.
		/// </summary>
		UnableToCreateSurveyLanguageFromAskiaCore,

	    /// <summary>
	    /// The required survey texts CSV file was not found or was invalid.
	    /// </summary>
	    SurveyTextsFileNotFoundOrInvalid,

	    /// <summary>
	    /// The required survey texts CSV file was provided but could not be read.
	    /// </summary>
	    SurveyTextsFileCouldNotBeRead,
		#endregion

		#region Routings
		/// <summary>
		///   Unable to create the routing in AskiaCore.
		/// </summary>
		UnableToCreateRoutingFromAskiaCore,

		/// <summary>
		///   Unable to save the routing in the Askia Design database.
		/// </summary>
	    UnableToSaveRoutingInDesignDatabase,

	    /// <summary>
	    ///   Unable to position the routing in the Askia Design database.
	    /// </summary>
	    UnableToPositionRoutingInDesignDatabase,

		/// <summary>
		///   Unable to delete the routing in AskiaCore.
		/// </summary>
		UnableToDeleteRoutingFromAskiaCore,

		/// <summary>
		/// The supplied routing action type value is 'null' when a value is required.
		/// </summary>
	    RoutingNullActionType,

	    /// <summary>
	    /// The supplied routing action type value is not a valid or recognised.
	    /// </summary>
	    RoutingInvalidActionType,

	    /// <summary>
	    /// The routing action type was null or invalid.
	    /// </summary>
	    RoutingActionTypeNullOrInvalid,

	    /// <summary>
	    /// The routing condition type was null or invalid.
	    /// </summary>
	    RoutingConditionTypeNullOrInvalid,

		/// <summary>
		/// The routing condition could not be set. AskiaCore rejected it.
		/// </summary>
		RoutingConditionInvalid,

		/// <summary>
		/// Unable to find the routing in the Askia Design database.
		/// </summary>
		RoutingNotFoundInDesignDatabase,

	    /// <summary>
	    /// Routing.IsDeleted was assigned a value instead of null.
	    /// This property cannot be set explicitly.
	    /// </summary>
	    RoutingIsDeletedValueSet,

	    /// <summary>
	    /// The supplied routing caption type value is not a valid or recognised.
	    /// </summary>
	    RoutingCaptionInvalidType,

	    /// <summary>
	    /// The supplied routing caption type is not valid for the action of this routing.
	    /// </summary>
	    RoutingCaptionInvalid,

		/// <summary>
		///   Unable to delete the routing targets for a routing in AskiaCore.
		/// </summary>
		UnableToDeleteRoutingTargetsFromAskiaCore,

	    /// <summary>
	    ///   Unable to set the action parameter value for a routing in AskiaCore.
	    /// </summary>
	    RoutingInvalidActionParameterValue,

		/// <summary>
		/// Unable to create a routing without the start question ID.
		/// </summary>
		RoutingStartQuestionIdNotSet,

		/// <summary>
		/// The ID of the routing is required but missing.
		/// </summary>
		RoutingIdNotSet,

	    /// <summary>
	    /// The IDs of the routings are required but missing.
	    /// </summary>
	    RoutingIdsNotSet,

		/// <summary>
		/// The target position of the routing(s) was not set.
		/// </summary>
		RoutingPositionNotSet,

	    /// <summary>
	    /// The start question of the routing(s) was not set.
	    /// </summary>
	    RoutingStartQuestionNotSet,

	    /// <summary>
	    /// The start type of the routing(s) was not set.
	    /// </summary>
		RoutingStartTypeNotSet,

		/// <summary>
		/// The start question for the routing could not be found using the supplied identifier.
		/// </summary>
		RoutingStartQuestionNotFound,

		/// <summary>
		/// AskiaCore was unable to identify the entities affected by the operation.
		/// </summary>
		RoutingUnableToGetAffectedEntities,

		/// <summary>
		/// AskiaCore rejected the supplied routing name.
		/// </summary>
		RoutingNameRejected,

	    /// <summary>
	    /// The routing start type was null or invalid.
	    /// </summary>
		RoutingStartTypeNullOrInvalid,
		#endregion

		#region RoutingTarget
		/// <summary>
		/// The supplied routing target type value is not a valid or recognised.
		/// </summary>
		RoutingTargetInvalidType,

	    /// <summary>
	    ///   Unable to create the scenario in AskiaCore.
	    /// </summary>
	    UnableToCreateRoutingTargetFromAskiaCore,

	    /// <summary>
	    ///   Unable to save the routing target in the Askia Design database.
	    /// </summary>
	    UnableToSaveRoutingTargetInDesignDatabase,

		/// <summary>
		///   Unable to delete the routing target in AskiaCore.
		/// </summary>
		UnableToDeleteRoutingTargetFromAskiaCore,

	    /// <summary>
	    ///   The response target ID value supplied is not valid.
	    /// </summary>
	    ResponseTargetIdInvalidValue,

	    /// <summary>
	    ///   The response target type value supplied is not valid.
	    /// </summary>
	    ResponseTargetTypeInvalidValue,

	    /// <summary>
	    ///   The response target type value supplied is null.
	    /// </summary>
	    ResponseTargetNullQuestionIdValue,
		#endregion

		#region PublishSurvey

	    /// <summary>
	    ///   The CcaWebServer could not be found or is not accessible to the user.
	    /// </summary>
	    CcaWebServerNotFound,
	    /// <summary>
	    ///   The item could not be found or is not accessible to the user.
	    /// </summary>
	    ItemDoesntExist,
		#endregion

		#region User
		/// <summary>
		///   The user could not be found in AskiaPortal.
		/// </summary>
		UserNotFoundInPortal = 70000,
		#endregion

		#region End
		/// <summary>
		///   No error.
		/// </summary>
		NoError = 80000,
	    /// <summary>
	    ///   Unspecified error.
	    /// </summary>
	    Unspecified = 80001,
		/// <summary>
		///   Unknown error.
		/// </summary>
		Unknown = 80002,
		#endregion
