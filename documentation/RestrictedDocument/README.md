# <a id="top">Restricted Document</a>
- [1. Features](#features)
  - [1.1. Restricted Document](#restricted_document)
    - [1.1.1. Restrict Un Allowed User From Document](#restrict_un_allowed_user_from_document_topic)
    - [1.1.2. Update Restricted Users List From File](#update_restricted_users_list_from_file_topic)
  - [1.2. Monitor Activity Events](#monitor_activity_events)
    - [1.2.1. Voting Events Can Be Hidden From Activity Page](#voting_events_can_be_hidden_from_activity_page_topic)

# 1. <a id="features">Features</a>
## 1.1. <a id="restricted_document">Restricted Document</a>
### 1.1.1. <a id="restrict_un_allowed_user_from_document_topic">Restrict Un Allowed User From Document</a>
If [Document.allowedUsers](../data_model.md#document_allowedusers) exists<br>
then only users defined in this list should be allowed to participate in the document discussion

If the list does not exist then anyone can view/edit the document. (current behaviour)

If current user is not in the allowed users list he cannot access the voting view
- From [Draft Page](../VotingPage/README.md#draft_page), when the user clicks on "Go To Discussion" button, he is redirected to [Welcome Page View](../VotingPage/README.md#welcome_page_view)
- For a user that is not logged in:<br>
From [Welcome Page View](../VotingPage/README.md#welcome_page_view), when the user clicks on "Go To Discussion" button, show login/signup popup.<br>
If the email of the user is not in [Document.allowedUsers](../data_model.md#document_allowedusers) list, after the user tries to signup/login a pop-up should appear, letting him know he is not allowed user in this document and should contact the document admin
- For a user that is logged in:<br>
If the email of the user is not in [Document.allowedUsers](../data_model.md#document_allowedusers) list, after click on "Go To Discussion" button a pop-up should appear letting him know he is not allowed user in this document and should contact the document admin
- Label: **goToDiscussionPopup**
  - he: '[ההשתתפות מותרת למורשים בלבד. אם אתם משתמשים מורשים נסו להתחבר דרך אימייל אחר. ליצירת קשר עם [מנהלי התהליך<mailto:info@consenz.co.il>'
  - en: 'Participation is restricted to allowed users, Try to login form a different email. Click [here]<mailto:info@consenz.co.il> to contact admin'

![restrict_un_allowed_user_from_document_mockup1](https://user-images.githubusercontent.com/5900841/107200426-5b587480-6a00-11eb-906d-34fe76bffa0a.png)

- [Welcome Page View](../VotingPage/README.md#welcome_page_view) and [Draft](../README.md#draft_definition) will be visible to all
- Cloud Firestore Rules may be involved
#### Implementation
- [allowedUsers validation and goToDiscussionPopup](https://github.com/wonderfloyd/Consenz/commit/c3d03284f285166807ba8857bf48fccebe35db3a)
- [Access Validation Fixes](https://github.com/wonderfloyd/Consenz/commit/9977159b263a056bb20c24c88cb7925e4d2ac9bd)
- [allowedUsers.includes(mailAddress) fix](https://github.com/wonderfloyd/Consenz/commit/d6928f19da4b22cf444208cdbfd450adb03f6ab4)
- [style fixes](https://github.com/wonderfloyd/Consenz/commit/e027736d0e5c5610cb14fe777442b0921bf40ad7)
- [participants count](https://github.com/wonderfloyd/Consenz/commit/95df471bed03dd4d4093521248d624a221fe7a99)
### 1.1.2. <a id="update_restricted_users_list_from_file_topic">Update Restricted Users List From File</a>
Allow an option to upload html or csv file of emails list to this field
- List file could be uploaded directly to the data base using firebase functionality
## 1.2. <a id="monitor_activity_events">Monitor Activity Events</a>
### 1.2.1. <a id="voting_events_can_be_hidden_from_activity_page_topic">Voting Events Can Be Hidden From Activity Page</a>
If the [Document.hideVoteEvents](../data_model.md#document_hidevoteevents) value is true, then hide voting events items from [Event Activity Page](../UpdateBell/README.md#event_activity_page)

![voting_events_can_be_hidden_from_activity_page_mockup1](https://user-images.githubusercontent.com/5900841/106575241-87797e80-6544-11eb-9a25-bd81de62513e.png)
#### Implementation
- [documentHideVoteEvents logic](https://github.com/wonderfloyd/Consenz/commit/48db4792a609af701c98d0653b2131bb8d89a838)
