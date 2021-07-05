# <a id="top"></a> Data Model
This is the Applications Data Model. It consist of four objects:  
- [User](#user)
- [Document](#document)
- [Section](#section)
- [Argument](#argument)
- [Comment](#comment)
- [ChangeEvent](#changeEvent)

## <a id="user">User</a>
| Field |  |  |  | Type | Description | 
| --- | --- | --- | --- | :--- | :--- |  
| displayName | | | | String
| created_at | | | | Date
| documents | | | | List (Documents) | all the documents that the user assign to
| notifications | isOn | | | Boolean | determine if mail notifications will be sent to he user<br> (will be on "false" if user unsubscribed)
| | mailAddress | | | String | email address of the user,<br>for sending notifications and for identification in log in.
| | mailNotificationFrequency | | | String | Frequency of mail notifications. Should be one of `event`, `daily`, `weekly`, `never` |
| | lastNotificationsTime | | | Date | The last time the current user watched the notifications page
| | msgRegistrationToken | | | String | Messaging token for push notifications |
| | documents | [documentId] |  newArgumentOrCommentNotification | Boolean | Notify the user on new arguments and comments for the document |
| | | | newDocumentVersionNotification | Boolean | Notify the user on new version of the document|
| | | | newEditSuggestionNotification | Boolean | Notify the user on new edit suggestion for the document |
| | | | newSectionSuggestionNotification | Boolean | Notify the user on a new suggestion for a section for the document |
| photoURL | | | | String | URL link to profile photo of user
## <a id="document">Document</a>
| Field | Type | Description | 
| --- | :--- | :--- |  
| about | String | Static text to describe the purpose of the discussion.<br>Can be edited for now only from firebase,<br>in th future will be edited from admin interface. 
| conditionalSupport | Boolean | 
| cons | List (Arguments) | 
| pros | List (Arguments) | 
| consensus_meter | String | A number between 0 to 1 that reflect the level of support<br>that the users gave to the current draft<br>by voting to the sections that has been accepted.<br>a consensus_meter of a document in an average of all "consenuses" (see next) and is updated every time a new consensus_meter is generated.
| consensuses | List (Numbers) | An array of the specifics consensus_meters for every accepted section.<br>When the delta pro-voters of a suggestions reach it's threshold (see next)<br>a new consensus_meter is generated according to this formula:<br>new consensus_meter = (1 - (con votes / pro votes)) * ((pro voters) / users of draft) 
| createdAt | Date | 
| divisionOfTopics | Boolean | Determine if the document draft can be divided to different topics.
| documentTopics | List (Strings)
| editors | List (Users) | Users that have admin authorization and can accept or reject suggestion by choosing to use their veto right.<br>In UI editors user will see, below voting buttons, a checkbox "use editor privilege".<br>If this checkbox is marked then editor user vote will determine the suggestion fate:<br> If voted pro the suggestion will be accepted, if voted con it will be denied,<br> Without considering the threshold, other voting and timer.
| sendNotifications | Boolean | Determine if mail notifications will be sent to all users of the document or not.
| threshold | Number | A number of pro voters minus con voters that require for accepting suggestion.<br>The threshold of all existing and new suggestions is set every time that a suggestions is accepted and a new consensus_meter is generated.<br>Threshold = consensus_meter * number of users of the document
| timer | Number | A time that set the deadline of suggestions from it's ceatedDate.
| title | String | The name of the document.
| updated_at | Date
| updated_by | List (Users)
| voteOnDocument | Boolean | A way for users to vote pro or con the current document draft as a general,<br> without voting for a specific suggestion.
| <a id="document_hidevoteevents">hideVoteEvents</a> | Boolean | If true then in Event Activity Page don't show voting events items
| allowedUsers | List (Users) | If exists, only users in the list are allowed to get access to document data
| mainThemeColor | String | Optional. A color hex code to serve as main color for all views in the document. Defaults to purple (`#69378e`).
## <a id="section">Section</a>
| Field | Type | Description | 
| --- | :--- | :--- |  
| <a id="section-topic">topic</a> | String
| content | String
| created_by | User (ref) | The user that published the first suggestion of the section
| owner | User (ref)
| updated_by | User(ref)
| documentId | Document(ref)
| parentSectionId | Section(ref) | If the section is an edit suggestion,<br>when accepted it's text will replace the section that parentSectionId refer to.
| accepted_at | Date
| created_at | Date
| deadline | Date
| updated_at | Date
| <a id="section_cons">cons</a> | Arguments | argument can be pro or con.<br>when user publish new argument his vote<br>will be considered according to the argument mode.<br> here are argument that connected to the votes.
| <a id="section_pros">pros</a> | Arguments 
| contentHtml | String
| deleted
| edited | | previous versions of the section.<br>will be shown in the section history page view.
| <a id="status">status</a> | Number | The voting status of the Suggestion<br>0 = in a vote<br>1 = accepted<br>2 = declined<br>3 = deleted (by voting)<br>4 = edit section suggestion on a vote for a parent section of status 1<br>5 = edit section suggestion accepted<br>6 = edit section suggestion declined<br>7 = edit section suggestion on a vote for a parent section of status 0<br>
| <a id="threshold">threshold</a> | Number | A number of pro voters minus con voters that require for accepting suggestion.<br>The threshold of all existing and new suggestions<br>is set every time that a suggestions is accepted and a new consensus_meter is generated.<br>Threshold = consensus_meter * number of users of the document
| timer | Number
| tag | String
| toDelete | List | If there is a suggestion to delete this section, its id will be shown here.
| <a id="to-edit">toEdit</a> | List | If there is a suggestions to edit this section, its ids will be shown here.
## <a id="argument">Argument</a>
### Note
In data model there is a distinguish between "argument" (relate to a section) and "comment" (relate to an argument). For the users, both objects are called "comment", and the difference is between comment on a section (="argument" in data model), and comment on a comment (="comment" in data model).

| Field | Type | Description |
| --- | :--- | :--- |
| content | String
| convinced | Users | "convinced" button is a way for users to express support of other users argument.<br>if user push "convinced" button of argument his vote will be the same as the argument mode - pro/con
| created_at | Date
| created_by | User (ref)
| documentId | Document (ref)
| owner | User (ref)
| sectionId | Section (ref)
| type | Boolean
| updated_at | Date
| updated_by | User (ref)
## <a id="comment">Comment</a>
| Field | Type | Description |
| --- | :--- | :--- |
| argumentId | String | Id of the argument this comment relates to
| content | String
| createdAt | Date
| created_at | Date
| created_by | User (ref)
| documentId | Document (ref)
| owner | User (ref)
| sectionId | Section (ref)

## <a id="changeEvent">ChangeEvent</a>
| Field | Type | Description |
| --- | :--- | :--- |
| createdAt | Date
| <a id="eventType">type</a> | String | The Type of the event:<br>- User Voted For Suggestion<br>- User Added New Argument<br>- User Added New Comment<br>- User Added New Section Suggestion<br>- User Added New Edit Section Suggestion<br>- New Section Suggestion Was Accepted<br>- New Edit Section Suggestion Was Accepted
| subType | String
| itemId | Section/Argument/Comment (ref) | The id of the item that was added/changed/voted/accepted
| creator | User (ref)
