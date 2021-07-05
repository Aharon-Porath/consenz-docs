# <a id="top">Consenz Update Bell & Activity Feed specifications</a> 
The details and mock ups of the different features that have to be developed

- [Update Bell](#update-bell)
- [Event Activity Page](#event_activity_page)
- [Event Types](#event-types)
- [Browser Push and Email Notifications](#browser-push-email-notifications)
- [Unsubscribe](#unsubscribe)
- [Pending Notifications Option](#pending_notifications_option)
- [E-mail Aggregation](#mails_aggregation)
- [Navigation Bar](#navigation_bar)

# 1. <a id="update-bell">Update Bell</a>
The goal is to inform the user about new changes in the document<br>
and give him a quick access to the Activity Page view with all recent changes

![Image20200708132620](https://user-images.githubusercontent.com/5900841/88152804-3be92e00-cc0d-11ea-9d35-1c5e90bb4a37.png)

## 1.1. Visual
- Location: Navigation Bar
- Image: Bell with a Counter at the left-top corner
## 1.2. Bell Counter
The amount of new notifications since the last time the user visited the [Notification Activity Page](#event_activity_page).
- After the user visits the activity page, the counter is reset to 0 for the user
- for users that are not logged in, the counter will show the amount of all activity of the document.
## 1.3. Click Action
Clicking on the bell leads to the [Notification Activity Page](#event_activity_page).
# 2. <a id="event_activity_page">Event Activity Page</a>
The goal of this page is to show notifications of all recent change events in the document<br>
and let the user click on an event and see the its details

![event_activity_page_mockup1](https://user-images.githubusercontent.com/12394551/86937632-27566180-c148-11ea-8b95-de0e7145a4de.png)

## 2.1. <a id="page_title_topic">Page Title</a>
- Dictionary parameter: **activityPageTitle**
  - he: 'פעילות אחרונה בדיון'
  - en: 'Last Activity'
## 2.2. <a id="events_feed_topic">Events Feed</a>
List of all document events. Each is represented with an Event Item Card consisting of the following:
### 2.2.1. <a id="reacting_user_element">Reacting User</a>
[User Avatar](../VotingPage/README.md#user_avatar_topic) (profile pic + user name) of the user that created the event 
### 2.2.2. <a id="created_at_element">Created At</a>
The value is according to the event:
- New item added: ([argument](../data_model.md/#argument) / [comment](../data_model.md/#comment) / [section](../data_model.md/#section)).created_at
- Voting event: [section](../data_model.md/#section).updated_at
- Edit/New Suggestion Accepted event: [section](../data_model.md/#section).acceptedAt
### 2.2.3. <a id="event_description_prefix_element">Event Description Prefix</a>
Prefix of event description based on the Notification type:
- [user voted for suggestion](#user-voted-for-suggestion-notification-text)
- [user added new argument](#user-added-new-argument-notification-text)
- [user added new comment](#user-added-new-comment-notification-text)
- [user added new section suggestion](#user-added-new-section-suggestion-notification-text)
- [user added new edit section suggestion](#user-added-new-edit-section-suggestion-notification-text)
- [new section suggestion was accepted](#new-section-suggestion-was-accepted-notification-text)
- [new edit section suggestion was accepted](#new-edit-section-suggestion-was-accepted-notification-text)
### 2.2.4. <a id="read_more_clickable_element">Read More Clickable</a>
Clickable link that that allow the user to dive into the details of the change event.
- Label
  - he: 'קרא עוד'
  - eb: 'Read more'
- On Click: Show in activity page the full text of the section/argument/comment, without loading a new page.
### 2.2.5. <a id="trash_icon_element">Trash icon</a>
  - Trash icon will displayed only on items that their reacting User is the logged in user (user can only delete his own activity event).
  - Clicking on the trash icon opens a popup to approve deletion.
    - he: 'למחוק פריט זה?'
      - yes: 'כן'
      - no: 'לא'
    - en: 'Delete this item?'
      - yes: 'Yes'
      - no: 'No'
  - If user click 'yes' the item will be removed from activity page display for all users. 
## 2.3. <a id="sorting_dropdown_topic">Sorting Dropdown</a>
Sorting options for the events feed
### Options:
- created at: from late to early
  > by default
  - he: 'הצג לפי זמני ארועים'
  - en: 'Created At'
- event of the user - the reacting user of the event is the user that logged in.
  - he: 'פעולות שלי'
  - en: 'My Events'
   
![notificationsSorting](https://user-images.githubusercontent.com/12394551/87117850-48bb6880-c282-11ea-9c2d-ed1bde984e38.png)
# 3. <a id="event-types">Event Types</a>
## 3.1. User Voted For Suggestion
### 3.1.1. Trigger Flow:
- Welcome Page [(Entering Page View)](../VotingPage/README.md/#entering-page-view) -> Proceed button click
- [Choose Topics Page](../VotingPage/README.md/#choose-topics-page-view) -> Topic To Discussion button click
- Voting Page ([New Votes Page](../VotingPage/README.md/#new-votes-page)) -> Vote Pro/Con button click
### 3.1.2. Data Model
When a user votes on a [section](../data_model.md/#section),<br>
Add [ChangeEvent](../data_model.md/#changeEvent):
- created_at: [section](../data_model.md/#section).updated_at
- type: "User Voted For Suggestion"
- subType: "voted pro" / "voted con"
- itemId: [section](../data_model.md/#section).id
- creator: Voting [User](../data_model.md/#user).id
### 3.1.3. <a id="user-voted-for-suggestion-notification-text">Activity Page Notification Text</a>
- Format
  - he:

        ...<suggestionTextPrefix> <userName>: לסעיף של <eventType> <reactingUserName> 
  - en:

        <reactingUserName> <eventType> on suggestion of <userName>: <suggestionTextPrefix>...
- eventType: [changeEvent](../data_model.md/#changeEvent).subType
  - voted pro
    - he: 'תמכ/ה ב'
    - en: 'voted pro'
  - voted con
    - he: 'הסתייג/ה מה'
    - en: 'voted con'
- reactingUserName: [changeEvent](../data_model.md/#changeEvent).creator (Voting User).
- suggestionTextPrefix: [section](../data_model.md/#section)([changeEvent](../data_model.md/#changeEvent).itemId).content prefix<br>
Text prefix of 'content' field of section data model.
- userName: [section](../data_model.md/#section)([changeEvent](../data_model.md/#changeEvent).itemId owner name

## 3.2. User Added New Argument
### 3.2.1. Trigger Flow:
    Welcome Page (Entering Page View) -> Proceed button click
    Choose Topics Page -> Topic To Discussion button click
    Voting Page (New Votes Page) -> Add New Argument button click (see screenshot)
    Voting Page, New Argumant Text Box -> Enter Text and Publish button click
    
![image](https://user-images.githubusercontent.com/5900841/89333620-e77a8f80-d69d-11ea-8ca0-16a912305488.png)

### 3.2.2. Data Model
When a user adds an argument to a suggestion [section](../data_model.md/#section),<br>
For each of the section registered users (registeredUser):<br>
Add [ChangeEvent](../data_model.md/#changeEvent):
- created_at: [argument](../data_model.md/#argument).created_at
- type: "User Added New Argument"
- itemId: [argument](../data_model.md/#argument).id
- creator: [User](../data_model.md/#user).id of Logged user that added the argument
- registeredUser: id of registeredUser
### 3.2.3. <a id="user-added-new-argument-notification-text">Activity Page Notification Text</a>
- Format
  - he:

        ...<argumentTextPrefix> :<userName> הגיב/ה לסעיף של reactingUserName 
  - en:

        <reactingUserName> added new argument on suggestion of <userName>: <argumentTextPrefix>...
        
- reactingUserName: [changeEvent](../data_model.md/#changeEvent).creator (Voting User).
- userName: [section](../data_model.md/#section)([changeEvent](../data_model.md/#changeEvent).itemId owner name
- argumentTextPrefix: [argument](../data_model.md/#argument)([changeEvent](../data_model.md/#changeEvent).itemId).content prefix<br>
Text prefix of 'content' field of argument data model.

## 3.3. User Added New Comment
A user adds an comment to a [section](../data_model.md/#section) or an [argument](../data_model.md/#argument)
### 3.3.1. Trigger Flow:
    Welcome Page (Entering Page View) -> Proceed button click
    Choose Topics Page -> Topic To Discussion button click
    Voting Page (New Votes Page) -> Add New Comment button click
    Voting Page, Add New comment Text Box -> Publish button click
    
### 3.3.2. Data Model
For each of the item(section or argument) registered users (registeredUser):<br>
Add [ChangeEvent](../data_model.md/#changeEvent)
- created_at: [comment](../data_model.md/#comment).created_at
- type: "User Added New Comment"
- subType: "Section" / "Argument"
- itemId: [comment](../data_model.md/#comment).id
- creator: [User](../data_model.md/#user).id of Logged user that added the comment
- registeredUser: id of registeredUser
### 3.3.3. <a id="user-added-new-comment-notification-text">Activity Page Notification Text</a>
- Format
  - he:

        ...<commentTextPrefix> :<userName> של <item>הגיב/ה ל <reactingUserName>
  - en:

        <reactingUserName> commented on <item> of <userName>: <commentTextPrefix>...
- item: [changeEvent](../data_model.md/#changeEvent).subType -  Section or Argument.
  - Section
    - he: 'סעיף'
    - en: 'section'
  - Argument
    - he: 'תגובה'
    - en: 'argument'
- reactingUserName: [changeEvent](../data_model.md/#changeEvent).creator (Voting User).
- userName: [section](../data_model.md/#section)([changeEvent](../data_model.md/#changeEvent).itemId owner name
- commentTextPrefix: [comment](../data_model.md/#comment)([changeEvent](../data_model.md/#changeEvent).itemId).content prefix<br>
Text prefix of 'content' field of comment data model.

## 3.4. User Added New Section Suggestion
A user added a Suggestion for a new [Section](../data_model.md/#section)
### 3.4.1. Trigger Flow:
    Welcome Page (Entering Page View) -> Proceed button click
    Choose Topics Page -> Topic To Discussion button click
    Voting Page (New Votes Page) -> Last Vote Page 
    Last Vote Page -> Add New Section button click
    Add New Section page -> Publilsh button click
or:

    Welcome Page (Entering Page View) / Summary Page -> Go to Draft button click
    Draft Page -> Add New Section button click
    Add New Section page -> Publilsh button click
### 3.4.2. Data Model
For each of the document registered users (registeredUser):<br>
Add [ChangeEvent](../data_model.md/#changeEvent):
- created_at: New [Suggestion](../data_model.md/#section).created_at
- type: "User Added New Section Suggestion"
- itemId: New [suggestion](../data_model.md/#section).id
- creator: [User](../data_model.md/#user).id of Logged user that added the suggestion
- registeredUser: id of registeredUser
### 3.4.3. <a id="user-added-new-section-suggestion-notification-text">Activity Page Notification Text</a>
- Format
  - he:

        ...<sectionTextPrefix> :<topic> פרסמ/ה הצעה לסעיף חדש בנושא <reactingUserName> 
  - en:

        <reactingUserName> Added a new section suggestion on <topic> topic: <sectionTextPrefix>...
- reactingUserName: [changeEvent](../data_model.md/#changeEvent).creator (Voting User).
- topic: [suggestion](../data_model.md/#section).topic field
- sectionTextPrefix: [section](../data_model.md/#section)([changeEvent](../data_model.md/#changeEvent).itemId).content prefix<br>
Text prefix of 'content' field of the new suggestion.

## 3.5. User Added New Edit Section Suggestion
A user added a new Edit Section Suggestion to replace existing [Section](../data_model.md/#section)
### 3.5.1. Trigger Flow:
    First scenario:
    Welcome Page (Entering Page View) -> Proceed button click
    Choose Topics Page -> Topic To Discussion button click
    Voting Page (New Votes Page) -> Edit Section Suggestions tab title click
    Voting Page, Edit Section Suggestions tab mode -> Add New Edit Suggestion button click
    Second scenario:: 
    Voting Page (New Votes Page) -> Vote Con Button click
    Voting Page (New Votes Page) -> Add New Edit Suggestion button click
    Voting Page, New Edit Suggestion Text Box -> Publish button click
   
For each of the section registered users (registeredUser):<br>
Add [ChangeEvent](../data_model.md/#changeEvent):
- created_at: New Edit [Suggestion](../data_model.md/#section).created_at
- type: "User Added New Edit Section Suggestion"
- itemId: New [suggestion](../data_model.md/#section).id
- creator: [User](../data_model.md/#user).id of Logged user that added the suggestion
- registeredUser: id of registeredUser
### 3.5.3. <a id="user-added-new-edit-section-suggestion-notification-text">Activity Page Notification Text</a>
- Format
  - he:

        ...<suggestionTextPrefix> :<topic>פרסמ/ה הצעה לשינוי סעיף בנושא <reactingUserName>  
  - en:

        <reactingUserName> Added a new edit section suggestion on <topic> topic: <suggestionTextPrefix>...
- reactingUserName: [changeEvent](../data_model.md/#changeEvent).creator (Voting User).
- topic: [suggestion](../data_model.md/#section).topic field
- suggestionTextPrefix: [suggestion](../data_model.md/#section)([changeEvent](../data_model.md/#changeEvent).itemId).content prefix<br>
Text prefix of 'content' field of the new suggestion.

## 3.6. New Section Suggestion Was Accepted
A [Section](../data_model.md/#section) Suggestion was accepted due to user pro votes.
### 3.6.1. Trigger Flow:
    Welcome Page (Entering Page View) -> Proceed button click
    Choose Topics Page -> Topic To Discussion button click
    Voting Page (New Votes Page) -> Vote Pro button click
    Threshold was 1, and after this vote reach 0 and an acceptedAt field wes added to section data model (see screenshot for example)
    ![image](https://user-images.githubusercontent.com/5900841/89334615-7b992680-d69f-11ea-997d-f035d72ac9aa.png)

### 3.6.2. Data Model
For each of the section and document registered users (registeredUser):<br>
Add [ChangeEvent](../data_model.md/#changeEvent):
- created_at: [section](../data_model.md/#section).acceptedAt
- type: "New Section Suggestion Was Accepted"
- itemId: (../The accepted [section](../data_model.md/#section).id
- creator: [User](../data_model.md/#user).id of User that created the suggestion. ([section](../data_model.mdedit /#section).owner)
- registeredUser: id of registeredUser
### 3.6.3. <a id="new-section-suggestion-was-acceted">
- Format
  - he:

        ...<suggestionTextPrefix>: <userName> התקבלה הצעה לסעיף חדש של
  - en:

        A new section suggestion of <userName> was accepted: <suggestionTextPrefix>...
- userName: [changeEvent](../data_model.md/#changeEvent).creator (User that created the suggestion).
- suggestionTextPrefix: [section](../data_model.md/#section)([changeEvent](../data_model.md/#changeEvent).itemId).content prefix<br>
Text prefix of 'content' field of section data model.
- userName: [changeEvent](../data_model.md/#changeEvent).creator (User that created the suggestion).
- suggestionTextPrefix: [section](../data_model.md/#section)([changeEvent](../data_model.md/#changeEvent).itemId).content prefix<br>
Text prefix of 'content' field of section data model.

A [Section](../data_model.md/#section) Suggestion was accepted due to user pro votes.
## 3.7. New Edit Section Suggestion Was Accepted
An Edit [Section](../data_model.md/#section) Suggestion was accepted due to user pro votes.
### 3.7.1. Trigger Flow:
    First scenario:
    Welcome Page (Entering Page View) -> Proceed button click
    Choose Topics Page -> Topic To Discussion button click
    Voting Page (New Votes Page) -> Vote Pro button click
    Threshold reach 0 and an acceptedAt field wes added to section data model)
    Second scenario:
    Welcome Page (Entering Page View) -> Proceed button click
    Choose Topics Page -> Topic To Discussion button click
    Voting Page (New Votes Page) -> Edit Section Suggestions tab title click
    Edit Section Suggestion vote Pro button click
    Threshold was 1, and after this vote reach 0 and an acceptedAt field wes added to section data model (see screenshot for example)
    ![image](https://user-images.githubusercontent.com/5900841/89335011-1a258780-d6a0-11ea-8cc7-3b4a3aec1a22.png)

For each of the section registered users (registeredUser):<br>
Add [ChangeEvent](../data_model.md/#changeEvent):
- created_at: edit suggestion [section](../data_model.md/#section).acceptedAt
- type: "New Edit Section Suggestion Was Accepted"
- itemId: The accepted edit suggestion [section](../data_model.md/#section).id
- creator: [User](../data_model.md/#user).id of User that created the edit suggestion. ([section](../data_model.md/#section).owner)
- registeredUser: id of registeredUser
### 3.7.3. <a id="new-edit-section-suggestion-was-accepted-notification-text">Activity Page Notification Text</a>
- Format
  - he:

        ...<suggestionTextPrefix> :לעריכת סעיף <userName> התקבלה הצעה של
  - en:

        An edit section suggestion of <userName> was accepted: <suggestionTextPrefix>...
- userName: [changeEvent](../data_model.md/#changeEvent).creator (User that created the suggestion).
- suggestionTextPrefix: [section](../data_model.md/#section)([changeEvent](../data_model.md/#changeEvent).itemId).content prefix<br>
Text prefix of 'content' field of section data model.

# 4. <a id="browser-push-email-notifications">Browser Push and Email Notifications</a>

## <a id="existing-notifications-code">**** Currently existing functionality ****</a>
- Most of the logic that triggers notifications is already implemented in [notificationsModule.ts](../../src/store/modules/notificationsModule.ts). __What is still missing is the rules for triggers__.
- The triggers logic is divided between `notificationsModule.ts` and the different components using it. `notificationsModule.notifySubscribers` is called in the component (see e.g [AddNew.ts](../../src/views/AddNew/AddNew.ts), line 268) with all the data needed to compute the recipients list.
- `notificationsModule.ts` uses methods from other vuex modules (e.g `usersModule.ts`) to construct the final message object to be sent.
- Push notifications require an agreement by the user and a registration token by which the user is identified. Prompting the user for agreement and storing his token in the DB, currently only happens in [Vote.ts](../../src/views/Document/Vote/Vote.ts) (line 359) and [Section.ts](../../src/views/Document/Section/Section.ts) (line 352), but it should happen every time the user is subscribed to a rule.
- Email notifications and push notifications are backed by the exact same logic. They diverge in `notificationsModule.sendNotifications` (line 264), where only push notifications are sent at the moment.
- Sending the notifications/emails is done by calling [serviceAPI.ts](../../src/services/serviceAPI.ts) which uses Axios to make HTTP requests.
- Push notifications are sent directly from the client by a call to Google's messaging API (see `serviceAPI.sendPushNotifications`).
- E-mail notifications are sent via Firebase Cloud Functions and currently work only in local development environment. See [functions/src/index.ts](../../functions/src/index.ts) and [functions/src/api/mailNotifications.ts](../../functions/src/api/mailNotifications.ts) for the code.

__*Important*: having the recipients list dependant on arguments passed to `notificationsModule.ts` at the component level is bad practice and hard to maintain. It should be refactored such as the component only passes a notification type argument and everything else is computed in one place (preferably `notificationsModule.ts`).__

![notifications lifecycle](../../documents/Notification_lifecycle.png)
![notifications flow](../../documents/notifications_flow.png)

#### To mock a push notification being sent follow these steps:
- Go to consenz-master test document - [https://consenz-master.netlify.app/document/0604-II/welcome](https://consenz-master.netlify.app/document/0604-II/welcome) and login.
- Repeat the previous step with a different browser and a different user.
- Make sure both users agreed to push notifications by clicking the update checkbox.
- With the first user, add a suggestion for a new section.
- Click on a different tab and minimize the browser (of the first user).
- With the second user (in the second browser), add a comment to the suggestion added with the first user.

__You should see a notification popping up on your screen!__  
_Note: this will work with any document in consenz-master, not just `0604-II`, but it might send notifications to some people..._  

#### To mock an e-mail notification being sent follow these steps:
- Run the app in firebase mode: 
```bash
npm run serve
```
- run the functions emulator: 
```bash
cd functions
npm run serve
```
- Make sure you uncomment the code in `serviceAPI.sendNotifications`.
- You'll need a user you have access to his email account be the owner of a section.
- Then, with a different user add an argument to the section owned by the first user. 

__The section owner should receive an e-mail (and probably a push notification as well).__

### Rules and Triggers table
| &#x2193; Rules / Triggers &#x2192; | Section status changed to approved | New edit section | New argument | New comment on an argument | New section in document |
|:---:|:---:|:---:|:---:|:---:|:---:|
| User is section's owner | &#x2713; | &#x2713; | &#x2713; | &#x2715; | &#x2715; |
| User marked section checkbox (1) | &#x2713; | &#x2713; | &#x2713; | &#x2715; | &#x2715; |
| User published new argument | &#x2713; | &#x2713; | &#x2713; | &#x2715; | &#x2715; |
| User published new edit suggestion | &#x2713; | &#x2713; | &#x2713; | &#x2715; | &#x2715; |
| Document new argument checkbox (2) | &#x2715; | &#x2715; | &#x2713; | &#x2715; | &#x2715; |
| Document section status checkbox (3) | &#x2713; | &#x2715; | &#x2715; | &#x2715; | &#x2715; |
| Document new edit suggestion checkbox (4) | &#x2715; | &#x2713; | &#x2715; | &#x2715; | &#x2715; |
| Document new section checkbox (5) | &#x2715; | &#x2715; | &#x2715; | &#x2715; | &#x2713; |
| User is owner of argument | &#x2715; | &#x2715; | &#x2715; | &#x2713; | &#x2715; |
| User comment on argument | &#x2715; | &#x2715; | &#x2715; | &#x2713; | &#x2715; |

![image](https://user-images.githubusercontent.com/5900841/102263664-4fc76080-3f1d-11eb-821c-fbecfe96abc1.png)

![image](https://user-images.githubusercontent.com/5900841/102264510-6d48fa00-3f1e-11eb-8998-698d3822dea7.png)

**Note**: In data model there is a distinction between "argument" (related to a section) and "comment" (related to an argument). For the users, both objects are called "comment", and the difference is between comment on a section (="argument" in data model), and comment on a comment (="comment" in data model).

## 4.1. Section Notifications
User subscribes for a section change notification.
### 4.1.1. Subscription Rules
- The user is owner (user ID is in "owner" field of the section data model).
- User mark notification checkbox of the section.
- User publish an argument on the section.
- User publish an edit suggestion for the section.
### 4.1.2. Data-Model
- Add section id as "true" to "notifications" -> "suggestionsNotifications" of user data model) (see screenshot for example)

![image](https://user-images.githubusercontent.com/5900841/89335396-a33cbe80-d6a0-11ea-9dd6-4f3f0d9a177c.png)


**Note**: For all users that are subscribed for a section or for a comment, the notifications checkbox should be marked as true. If user unchecked the checkbox unsubscribe him from all notifications, until he marked the checkbox again (i.e., if user unchecked and then publish a comment, don't subscribe).  

### 4.1.3. Notification Triggers and Message Text
## 4.1.3.1 Texts for push notifications
As eventNotification labales used in activity feed page.

## 4.1.3.2 Texts for email notifications
- The section status changed to "approved"
  - en
    - Title: "A suggestion that you follow got accepted"
    - Body: "A suggestion that you follow got accepted and the document "[document Title]" had been updated accordingly.<br>The section that was added: "[section content]"<br>To watch current draft click here <+link to draft>"
  - he
    - Title: "הצעה לסעיף שעקבת אחריו התקבלה"'
    - Body: הצעה לסעיף שעקבת אחריה התקבלה, והמסמך "[document Title]" עודכן בהתאם<br>נוסח ההצעה:"[section content]"<br>לצפייה בטיוטת המסמך העדכנית לחצו כאן<+link to draft>"
- A new edit section is created<br>
  (a new field added in section data model "toEdit" field).
  - en
    - Title: "A new edit suggestion for section that you follow"
    - Body: "[section owner user name] published a new edit suggestion for a section that you follow.<br>The original text: [parent section content]<br>The edit suggestion: [edit section content].<br>To watch, comment or vote for the new suggestion<br>click here [link to section single page]"
  - he
    - Title: "פורסמה הצעה לשינוי סעיף שעקבת אחריו"
    - Body: "[section owner user name] פרסמ/ה הצעה לשינוי סעיף.  נוסח הסעיף המקורי: '[parent section content]'<br>    נוסח הצעת העריכה:  '[section content]'<br>  לתמיכה, הסתייגות או תגובה להצעה לחצו כאן [link to section single page]"  
- A new argument is created<br>
(an argument that the section id is in argument data model "sectionId" field).
  - en
    - Title: "A new comment in a discussion that you follow:
    - Body: "[comment / argument owner User Name] has publish a new comment:'[argument / comment content]'<br>To see new comment click here [+link to section page, view will scroll to the new argument/comment]"
  - he
    - Title: "תגובה חדשה לדיון בהשתתפותך:
    - Body: "[comment / argument owner User Name] הגיב/ה בדיון שהשתתפת בו: '[argument / comment content]'<br>  לדיון [+link to section page, view will scroll to the new argument/comment]"
- A new comment on an argument that the user comment on is created<br>.
  - en
    - Title: "A new comment in a discussion that you follow:
    - Body: "[comment owner User Name] has publish a new comment:'[comment content]'<br>To see new comment click here [+link to section page, view will scroll to the new comment]"
  - he
    - Title: "תגובה חדשה לדיון בהשתתפותך:
    - Body: "[comment owner User Name] הגיב/ה בדיון שהשתתפת בו: '[comment content]'<br>  לדיון [+link to section page, view will scroll to the new comment]"
- A new comment on an argument that the user is it's owner is created<br>
  (a comment that it's argumentId field is an argument that the user is it's owner)
  - en
    - Title: "A new comment in a discussion that you follow:
    - Body: "[comment owner User Name] has publish a new comment:'[comment content]'<br>To see new comment click here [+link to section page, view will scroll to the new comment]"
  - he
    - Title: "תגובה חדשה לדיון בהשתתפותך:
    - Body: "[comment owner User Name] הגיב/ה בדיון שהשתתפת בו: '[comment content]'<br>  לדיון [+link to section page, view will scroll to the new comment]"

## 4.2. Document Notifications
User subscribes for a document change notification.

### 4.2.1. Subscription Configuration
- The user will get notification according to his subscription to notifications of the document.<br>
i.e. if the notification user configuraiton flag is set to true
- Data-Model Flags path: [User].updateObject.notifications.documents.[documentId]

| Event | Flag Parameter | 
| --- | :--- |
| New Argument is Added | newArgumentOrCommentNotification
| Section Status Changed to Approved | newDocumentVersionNotification
| New Edit Section is Created | newEditSuggestionNotification
| New Section is Created | newSectionSuggestionNotification

### 4.2.2. Action:
send an email/push notification

## 4.3. Push Notification Action
### 4.3.1. Offline Mode
Send an Email with Notification text and control buttons
- use Firebase to send mail
- Try to use code from functions/src/api/mailNotifications.ts
### 4.3.2. Web Mode
Use browser option (firefox and chrome) push notifications to show pop-up Window with Notification text and control buttons.
Click on push notification pop-up will open browser tab with the relevant section page. 

# 5. <a id="unsubscribe">Unsubscribe</a>
## 5.1. Unsubscription method
2 unsubscribe buttons in all mail notifications
- Will show at the bottom of page
- on minimal font size - 8 or 9.
### Section unsubscribe:
Text on button:
- en : "Unsubscribe from updates of this section"
- he : "אל תשלחו לי עוד עדכונים מדיון על סעיף זה"
If user clicks section unsubscribe button, open section page, and remove check from notifications checkbox, 
and show snack bar on buttom of the page with text:
- en: "You have been unsubscribed of updates for this section"
- he: "לא יישלחו עוד עדכונים על סעיף זה"

### General unsubscribe:
Text on button:
- en: "Unsubscribe from all updates"
- he: "הסרה מרשימת התפוצה"
For document unsubscribe button, open summary page, and remove check from all notifications, and show 
Pop up wih text:
- en: "You have been unsubscribed"
- he: "לבקשתך, לא יישלחו עוד עדכונים"

# 6. <a id="pending_notifications_option">Pending Notifications Option</a>
With this option notifications are first sent to admin user in order to approve sending to all users.
## 6.1. Data Model
Add to [Document](../data_model.md/#document) a new field - "pendingNotification"
- Type: Boolean
- If true then all notifications will be sent first to admin
   - Email is sent to all editors of the document (User[editor].email)
## 6.2. Mail
- Notification Text
- "Send" button - when the admin user clicks the Send button it sends notifications to all users.

# 7. <a id="mails_aggregation">Mails aggregation</a>
User could choose from those 3 options when email notifications will be sent:
1. Every time new event is created (as push notifications)
2. Once a day
3. Once a week
4. Never

If user choose option 2 or 3 then all events that he subscribed to will be aggregate into one email that will be sent according to his choosing, daily - at 17:00 UTC+2, weekly - at Thursday.  
In `functions/src/index.ts` you'll find an example function `runOnSchedule` that logs the email of the first user in the users collection every 5 minutes.  
__Note: there's no emulator for `firebase.functions.pubsub`, so you'll have to deploy the functions to test functions run on schedule.__ 
## 7.1 Email template 
If there is more then 1 event then email title will be:
  he: "סיכום האירועים האחרונים במסמך <document title>"
  en: "Last events in the discussion on document <document title>"
## 7.2. Data Model
In [DataModel.User.notifications](../data_model.md#user) a field named `mailNotificationFrequency` will have one the following string values to store the user's mail prefrences:
| Value | description |
| :--- | :--- |
| event | The user will receive the email with the push notification once the event is triggered |
| daily | The user will recieve an aggregation of daily mails once a day |
| weekly | The user will recieve an aggregation of weekly mails once a week |
| never | The user doesn't want to recieve any e-mail notifications |
## 7.3 Email preferences manager UI: 
By clicking on user profile pic on navbar, display below "sign out" button:
**Title:**
    He. "ניהול עדכונים במייל"
    En. "Notifications manager"
Options list (will be showed as drop down after click on "Notifications manager", with a checkbox for every option):
1. He. "שלחו לי עדכון על כל אירוע חדש"
    En. "Send me an email for every event"
2. He. "שלחו לי עדכונים פעם ביום"
    En. "Send me an email once a day"
3. He. "שלחו לי עדכונים פעם בשבוע"
    En. "Send me an email once a week"
4. He. "הסרה"
    En. "Unsubscribe me" 

By default option 2 will be marked as "true".

![image](https://user-images.githubusercontent.com/5900841/102071348-0554bf80-3e09-11eb-9a04-fb866c3942fe.png)

## 7.4 Aggregation Logic
There are two intervals at which aggregated mails are sent: daily and weekly. The following logic applies to both, with one difference, i.e the time interval.  
The aggregation logic relies on the `EventChange` Firestore collection which holds all the events.  
At each interval, the following logic is executed:
- Get all new events since last interval, __except for voting events, which do not trigger a notification.__
- Init an empty object (recipients objcet) to later store a list of events to be sent to each user. 
- Iterate over all events since last interval. For each event do:
  - Compute all recipietns for the event.
  - For each recipient of the event do:
    - Check if the user is in the recipients objcet:
      - If user exists in recipients objcet - add event to the user's event list.
      - If user doesn't exists - add the user to the obejct with the evnt in his list.
- For each user in the recipients object, send an email listing all the events since last interval (all the events the user have in his event list in the recipient object).


# 8. <a id="navigation_bar">Navigation Bar</a>
- [User Menu](../VotingPage/README.md#user-menu)
- Document Title
  - Taken from [Document](../data_model.md#document).title
- [Updates Bell](README.md)
- User Indication (Profile Pic or Sign-in button
  - User Signed-in: Show Profile Pic
    - Taken from [User](../data_model.md#user).photoURL
    - Clicking the profile pic opens sign-out option
      - he: "התנתקות"
      - en: "Sign out"
  - User is not Signed-in: Sign-in Button
    - he: "התחברות", en: "Sign in"
    - Clicking the Sign-in button opens login pop up.
      
## 8.1. Navigation Sub Panel
Below the navigation panel there is a transparent sub panel that shows the page name and the back button.
- Page Name - by field/text (as in current header panel of pages)
  - Welcome page: welcomeTitle (welcomeTitle taken from Document.documentWelcome.welcomeTitle)
  - Choose Topics page: document.documentTopics.documentTopicsTitle
  - Vote page / Single suggestion page
    - he: "דיון בהצעה"
    - en: "Suggestion Discussion"
  - Draft page
    - he: "טיוטת המסמך"
    - en: "Current Draft"
  - Edit suggestion feed page
    - he: "הצעות לעריכת סעיף X"
    - en: "Edit Suggestion for section X"
  - History page
    - he: "היסטוריית סעיף X"
    - en:"Section X History"
- Back Button
  
![image](https://user-images.githubusercontent.com/5900841/86739067-45d03600-c03e-11ea-8d6a-b18946728996.png)
