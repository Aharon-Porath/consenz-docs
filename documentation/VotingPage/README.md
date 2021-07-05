# <a id="top">Voting Page</a>
New Navigation Flow.<br>
The details and mock ups of the different pages that have to be developed
- [1. Notes](#notes)
  - [Site Language](#site_language_note)
  - [Design and Visual](#design_and_visual_note)
  - [Admin Edited Text](#admin_edited_text_note)
- [2. Pages](#pages)
  - [2.1. Welcome Page View](#welcome_page_view)
    - [2.1.1. Welcome Text](#welcome_text_topic)
    - [2.1.2. Proceed to Choose Topic](#proceed_to_choose_topic_topic)
    - [2.1.3. User Menu](#user_menu_topic)
    - [2.1.4. Bread Crumbs](#bread_crumbs_topic)
  - [2.2. Choose Topics Page View](#choose_topics_page_view)
    - [2.2.1. Topics list](#topics_list_topic)
    - [2.2.2. Proceed to Votes](#proceed_to_votes_topic)
    - [2.2.3. Mark All Checkbox](#mark_all_checkbox_topic)
    - [2.2.4. User Menu](#user_menu_topic)
    - [2.2.5. Bread Crumbs](#bread_crumbs_topic)
  - [2.3. Voting Page](#voting_page)
    - [2.3.1. Topic Title](#topic_title_topic)
    - [2.3.2. Section Proposal](#section_proposal_topic)
    - [2.3.3. Voting Buttons Section](#voting_buttons_section_topic)
    - [2.3.4. Voting Counters](#voting_counters_topic)
    - [2.3.5. Suggestion Navigation Buttons](#suggestion_navigation_buttons_topic)
    - [2.3.6. Arguments Section](#arguments_section_topic)
    - [2.3.7. Get Notifications Check Boxes](#get_notifications_check_boxes_topic)
    - [2.3.8. User Menu](#user_menu_topic)
    - [2.3.9. Bread Crumbs](#bread_crumbs_topic)
  - [2.4. Summary Page](#summary_page)
    - [2.4.1. End Text](#end_text_topic)
    - [2.4.2. Notifications Panel](#notifications_panel_topic)
    - [2.4.3. Go To Draft Button](#go_to_draft_button_topic)
    - [2.4.4. User Menu](#user_menu_topic)
    - [2.4.5. Bread Crumbs](#bread_crumbs_topic)
  - [2.5. Draft Page](#draft_page)
    - [2.5.1. Go to Suggestions Page](#go_to_suggestions_page_topic)
    - [2.5.2. Sections Overview](#sections_overview_topic)
    - [2.5.3. Document Title](#document_title_topic)
    - [2.5.4. Document Menu](#document_menu_topic)
    - [2.5.5. User Menu](#user_menu_topic)
- [3. Topics](#topics)
  - [3.1. User Menu](#user_menu_topic)
  - [3.2. Bread Crumbs](#bread_crumbs_topic)
  - [3.3. User Avatar](#user_avatar_topic)
  - [3.4. Timestamp](#timestamp_topic)

# 1. <a id="notes">Notes</a>
## 1.1 <a id="site_language_note">Site Language (Internationalization)</a>
- The current pages are coded with <b>Hebrew</b> labels hard-coded (very bad) in the vue html files
- The labels of the new pages should come from an app-dictionary key-value file, so it would be possible to support both English and Hebrew languages.
- The freelancer need to create only the English dictionary file that is used by the new pages.
- In the review step of each milestone, we may change the dictionary texts<br>
and add the Hebrew dictionary file based on the english dictionary, in order to check how it looks.
- it should be easy to configure the application to work with any dictionary.
## 1.2 <a id="design_and_visual_note">Design and Visual</a>
- The specifications and page mock-ups do not go into design details but only define the logics and general looks of the pages.
- The freelancer has the flexibility to design the pages as he sees fit, following the specification's technical requirements.
## 1.3 <a id="admin_edited_text_note">Admin Edited Text</a>
- some of the elements take their text from data fields that the Admin edits. (like Welcome Text)
- There is No need to support Admin API for updating admin data.<br>
Just edit the json mock data and start the application with the mock data containing any needed fields.
# 2. <a id="pages">Pages</a>
## 2.1. <a id="welcome_page_view">Welcome Page View</a>
The goal is to introduce the user to [document discussion](../README.md#document_definition) process,<br>
Explain the document issues and encourage her to sign up and participate.
### 2.1.1. <a id="welcome_text_topic">Welcome Text</a>
Static text, Edited by Admin user, represents overview. May include discussion preview
### 2.1.2. <a id="proceed_to_choose_topic_topic">Proceed to Choose Topic</a>
Proceed to choose [Topic](../README.md#topic_definition) Clickable (Button, Link, ect.)
- Page view shifts to [Choose Topics Page View](#choose_topics_page_view)
### 2.1.3. [_User Menu_](#user_menu_topic)
### 2.1.4. [_Bread Crumbs_](#bread_crumbs_topic)
### Mockups
The mockups are presented in two languages: english and hebrew

![welcome_page_view_mockup1](https://user-images.githubusercontent.com/12394551/71320184-873d3180-24b0-11ea-89ad-37513f589a34.png)

![welcome_page_view_mockup2](https://user-images.githubusercontent.com/42510547/70627786-80e8c300-1c2f-11ea-93f3-33f3a6ffe004.png)
- This mockup is missing the User Menu and Bread Crumbs elements
## 2.2. <a id="choose_topics_page_view">Choose Topics Page View</a>
The goal is to give the user an option to choose the topics relevant to her.
This page contains the topics list for the [current Document](../README.md#document_definition).<br>
The list should be a multiple selection checkbox,<br>
where the user can select either one, some, or all of the options.<br>
The default mode is that the "view all topics" option is marked.<br>
The [Proceed to Votes](#proceed_to_votes_topic) button leads to the [Voting Page](#voting_page).<br>
If no option is selected the user will go through all of the vote Suggestions in the [Document](../README.md#document_definition).<br>
Otherwise he'll go through vote suggestions specific to the Topics selected.
### __Variables__:
- topicsSelectedList - List of all Topics selected by the user
### 2.2.1. <a id="topics_list_topic">Topics list</a>
List of the topics in the document that are up for a vote.<br>
each one can be marked with a checkbox
- Each item in the list is the topic string label and a checkbox<br>
that if marked then the topic is added to the topicsSelectedList list.
### 2.2.2. <a id="proceed_to_votes_topic">Proceed to Votes</a>
A button that leads to the [Voting Page](#voting_page)
- If the user selected some topic (topicsSelectedList Not Empty)<br>
then the [Voting Page](#voting_page) will be in __Specific [Topic](../README.md#topic_definition)__ mode.
- If the user did not select any topic (topicSelectedList Empty)<br>
then the [Voting Page](#voting_page) will be in __View All Topics__ mode.
### 2.2.3. _Mark All Checkbox_
### 2.2.4. [_User Menu_](#user_menu_topic)
### 2.2.5. [_Bread Crumbs_](#bread_crumbs_topic)
### Mockups

![choose_topics_page_view_mockup1](https://user-images.githubusercontent.com/42510547/70627781-7fb79600-1c2f-11ea-8b7b-912ab69e9484.png)

![choose_topics_page_view_mockup2](https://user-images.githubusercontent.com/12394551/71320192-9623e400-24b0-11ea-93e9-a452181eaf3c.png)
- This mockup is missing the [User Menu](#user_menu_topic) and [Bread Crumbs](#bread_crumbs_topic) elements

![choose_topics_page_view_mockup3](https://user-images.githubusercontent.com/12394551/70518786-9c769f80-1b43-11ea-801d-035e9999adf8.png)
- This mockup contains also the [User Menu](#user_menu_topic) and [Bread Crumbs](#bread_crumbs_topic) elements
## 2.3. <a id="voting_page">Voting Page</a>
- This page presents all [Section Suggestions](../data_model.md#section) that are up for voting
- Either of New Sections or Edit Suggestions of existing sections
- One suggestion in a page view
- The Suggestions are presented to the user according to the [Most Agreed Upon](../logics.md#most_agreed_upon) sorting algorithm and the user selections in the Choose Topics page
- The user can navigate between the suggestions that stand for a vote
- When the user is finished voting on all open Suggestions he's redirected to the [Summary Page](#summary_page)
The page displays the [Section Proposal](#section_proposal_topic) to be voted upon,<br>
the creator [User Avatar](#user_avatar_topic), publication [Timestamp](#timestamp_topic),<br>
[Voting Buttons Section](#voting_buttons_section_topic), [Voting Counters](#voting_counters_topic), [Suggestion Navigation Buttons](#suggestion_navigation_buttons_topic),<br>
[Arguments Section](#arguments_section_topic) and [Get Notifications Check Boxes](#get_notifications_check_boxes_topic).

![voting_page_mockup1](https://user-images.githubusercontent.com/12394551/75106569-daee0780-5626-11ea-9ed3-669ff2ea52fe.png)
### 2.3.1. <a id="topic_title_topic">Topic Title</a>
[Section topic](../data_model.md#section_topic)
### 2.3.2. <a id="section_proposal_topic">Section Proposal</a>
The proposed [Section](../README.md#section_definition) text, [User Avatar](#user_avatar_topic) of proposing user and the published [Timestamp](#timestamp_topic)
- Label: **newSectionSuggestion**
  - he: 'הצעה לסעיף חדש'
  - en: 'New Section Suggestion'
#### 2.3.2.1. <a id="proposed_section_text_element">Proposed Section Text</a>
[Section contentHtml](../data_model.md#section_contenthtml)
#### 2.3.2.2. <a id="timestamp_element">Timestamp</a>
[Section created_at](../data_model.md#section_created_at)
[Timestamp](#timestamp_topic)
#### 2.3.2.3. <a id="user_avatar_element">User Avatar</a>
[User Avatar](#user_avatar_topic)
- should be as in existing **/document/springfield/section** implementation

The visual element is already implemented and can be seen [here]().<br>
**The code should be reused**

![section_proposal_mockup1](https://user-images.githubusercontent.com/12394551/74959235-e2d55e00-5412-11ea-998d-1de3fcdf3b71.png)
### 2.3.3. <a id="voting_buttons_section_topic">Voting Buttons Section</a>
- Voting buttons of current suggestion
- Float buttons, Shown regardless of scrolling page state
- All buttons actions follows the [User Connected Rule](../logics.md#user_connected_rule)
#### 2.3.3.1. <a id="vote_button_-_pro_element">Vote Button - Pro</a>
The user Press the Pro button.<br>
The Action executes the existing [Vote Pro](../undefined/README.md#vote_logic) logic.<br>
**The logic code should be reused**
- Operation: Add current user id - [Section pros](../data_model.md#section_pros)
- Label: **proButton**
  - he: 'בעד'
  - en: 'Pro'
#### 2.3.3.2. <a id="vote_button_-_con_element">Vote Button - Con</a>
The user Press the Con button.<br>
The Action executes the existing [Vote Con](../undefined/README.md#vote_logic) logic.<br>
**The logic code should be reused**
- Operation: Add current user id - [Section cons](../data_model.md#section_cons)
- Label: **conButton**
  - he: 'נגד'
  - en: 'Con'

![vote_button_con_mockup1](https://user-images.githubusercontent.com/12394551/74960280-b6224600-5414-11ea-9e60-018c22dd42f1.png)
#### <a id="vote_logic">Vote Logic</a>
Voting Pro/Con logic is already implemented.<br>
see example in [here](https://new_votes_page.netlify.com/document/springfield/section?sectionById=wLl23iX4gZCoQl11JqEV&index=1)

![vote_logic_mockup1](https://user-images.githubusercontent.com/12394551/74848127-0e3b4880-5340-11ea-963c-e9ac62777799.png)

![vote_logic_mockup2](https://user-images.githubusercontent.com/12394551/74848141-12676600-5340-11ea-8141-b1692dab499d.png)
#### 2.3.3.3. <a id="vote_con_argument_text_area_element">Vote Con Argument Text Area</a>
- Text Area and a publish button that let the user, following his Con [Vote](../README.md#vote_definition), add his argument about his Con Vote
- This element appears only if the user voted Con (clicked the [Vote](../README.md#vote_definition) Con button)
##### Labels
- Title: **voteConArgumentTitle**
  - he: 'הוספת הסתייגות'
  - en: 'Add Con Argument'
- Publish Button: **voteConArgumentButton**
  - he: 'פרסום והצבעה'
  - en: 'Publish Con Argument'

![vote_con_argument_text_area_mockup1](https://user-images.githubusercontent.com/12394551/75015850-4e124500-5492-11ea-9f7d-28e09c95630f.png)
- When the user press the 'Publish' button, a new Con [Argument](../README.md#argument_definition) is added to the suggestion section.<br>
The new argument should appear first in the arguments section
- **The text area elements and Publish logic should reuse the existing Add Con [Argument](../README.md#argument_definition) logic**
- In the existing logic when the user adds a Pro/Con argument, it is automatically counted as a Pro/Con voting respectively
- The requirement for the [Voting Page](#voting_page) is to show the 'Add Argument' text box in the existing page under the vote buttons only in case the user voted Con. Then, if the user adds an argument, it is not needed to do the voting logic again as in the existing implementation, only the add argument logic.
#### <a id="existing_add_con_argument_logic">Existing Add Con Argument Logic</a>
Adding a Con/Pro Argument logic and elements are already implemented in other existing page.<br>
see example in [here](https://new_votes_page.netlify.com/document/springfield/section?sectionById=wLl23iX4gZCoQl11JqEV&scrollId=k6ui5ilh&scrollTo=argument)

![existing_add_con_argument_logic_mockup1](https://user-images.githubusercontent.com/55399150/74917324-00cd9f00-53d0-11ea-905c-74559087969a.png)

![existing_add_con_argument_logic_mockup2](https://user-images.githubusercontent.com/55399150/74917358-0cb96100-53d0-11ea-816c-5c7b5325742d.png)

![existing_add_con_argument_logic_mockup3](https://user-images.githubusercontent.com/55399150/74917388-14790580-53d0-11ea-9718-4f36cd3e6fc6.png)

![existing_add_con_argument_logic_mockup4](https://user-images.githubusercontent.com/55399150/74917411-1cd14080-53d0-11ea-92b9-bf760f30ea7b.png)
#### 2.3.3.4. <a id="add_new_edit_suggestion_element">Add New Edit Suggestion</a>
- A button that opens a box for adding edit section suggestion text
- This element appears only if the user voted Con (clicked the [Vote](../README.md#vote_definition) Con button)
- Position: under the [Vote Con Argument Text Area](#vote_con_argument_text_area_element) element
- Label: **addNewEditSuggestionButton**
  - he: 'הוסף הצעה חדשה'
  - en: 'Add a new suggestion'

![add_new_edit_suggestion_mockup1](https://user-images.githubusercontent.com/12394551/75021765-971bc680-549d-11ea-905e-8324e60bf055.png)
#### 2.3.3.5. <a id="new_edit_suggestion_section_element">New Edit Suggestion Section</a>
When the user click on the [Add New Edit Suggestion](#add_new_edit_suggestion_element) button. these elements appear
- Editable text box contains the text of the section content
- a "Publish" grayed un-active button
##### Labels
- Original Section Text: **originalSectionText**
  - he: 'נוסח הסעיף המקורי'
  - en: 'Original section text'
- Original Section Text: **mySectionProposal**
  - he: 'נוסח ההצעה שלי'
  - en: 'My Section Proposal'
- Add Button Label: **publishNewEditSuggestionButton**
  - he: 'הוספה'
  - en: 'Publish'

![new_edit_suggestion_section_mockup1](https://user-images.githubusercontent.com/12394551/75033867-8b87ca00-54b4-11ea-820b-92b93d5f8142.png)
- The user can change text, then the "publish" button becomes active and colored
- After clicking "publish" the text will be added as a [New Edit Suggestion](#new_edit_suggestion_element)
- The page renders to show the new suggestion, with 1 Pro vote, of the creating user
- A [Section](../README.md#section_definition) data-model document is created:


    {
      "id": "[Generated]",
      "parentSectionId": "[id of original section]",
      "createdAt": "[Current Date]",
      "created_at": [Current Date],
      "cons": [],
      "pros": [
        "[id of current user]"
      ],
      "created_by": "[id of current user]",
      "owner": "[id of current user]",
      "content": "[New Text Suggesiton]",
      "status": 4, (Change existing section, on vote)
      "threshold": [Document.threshold} (according documentId)
      "documentId": [Document.id],
      "topic": [Document.topic],
    }
##### Existing implementation
- The 'Add New Edit Suggestion' logic and elements are already implemented in other existing page and **the code should be reused**
- see example in [here](https://new_votes_page.netlify.com/document/springfield/section?sectionsByStatus=4&index=1&id=J11Yn1UkNDQcpxtaKyh6)
- Press the + button

![new_edit_suggestion_section_mockup2](https://user-images.githubusercontent.com/55399150/74929430-1fd62c00-53e4-11ea-9ede-949f8af1efcd.png)

![new_edit_suggestion_section_mockup3](https://user-images.githubusercontent.com/55399150/74929457-2e244800-53e4-11ea-98ef-3dbd9e713128.png)
- Change the original section text and press the Add button

![new_edit_suggestion_section_mockup4](https://user-images.githubusercontent.com/55399150/74929529-5f047d00-53e4-11ea-98eb-0394dc5b3c88.png)

![new_edit_suggestion_section_mockup5](https://user-images.githubusercontent.com/55399150/74929573-75123d80-53e4-11ea-9304-e6e631831703.png)
- Press the 'Add without an Argument' button

![new_edit_suggestion_section_mockup6](https://user-images.githubusercontent.com/55399150/74929606-8ce9c180-53e4-11ea-9110-18b1d02380e3.png)

![new_edit_suggestion_section_mockup7](https://user-images.githubusercontent.com/55399150/74929676-adb21700-53e4-11ea-90cd-bd42054e97ce.png)
- The new suggestion appears in the suggestions page

![new_edit_suggestion_section_mockup8](https://user-images.githubusercontent.com/55399150/74929733-c6bac800-53e4-11ea-8452-412caf3f8789.png)
### 2.3.4. <a id="voting_counters_topic">Voting Counters</a>
Pro and Con Counters of current suggestion<br>
The Counters are displayed on the Voting buttons and show current state of voting counters
#### 2.3.4.1. <a id="pro_counter_element">Pro Counter</a>
- Operation: count (length) - [Section pros](../data_model.md#section_pros)
#### 2.3.4.2. <a id="con_counter_element">Con Counter</a>
- Operation: count (length) - [Section cons](../data_model.md#section_cons)
### 2.3.5. <a id="suggestion_navigation_buttons_topic">Suggestion Navigation Buttons</a>
Navigation buttons that allow the user to navigate between suggestions up for a vote according to the [Most Agreed Upon](../logics.md#most_agreed_upon) sorting algorithm and the user selections in the Choose Topics page.<br>
There are 2 buttons:
#### 2.3.5.1. <a id="next_suggestion_button_element">Next Suggestion Button</a>
- Label: **nextSuggestion**
  - he: 'הבא >>'
  - en: 'Next >>'
- Starting with greyed out button.<br>
The user can still press the button and navigate to the next suggestion.
- After the user votes the button is highlighted to indicate the user should press it and move to next suggestion
- When the user press the 'Next Suggestion' button the page renders to the next suggestion for voting
- The next suggestion is according to the [Most Agreed Upon](../logics.md#most_agreed_upon) sorting.
- If current shown suggestion is the last suggestion, then the user is transferred to the [Summary Page](#summary_page)
#### 2.3.5.2. <a id="back_button_element">Back Button</a>
Change page view back to previous suggestion<br>
If the user is in the first suggestion and press the [Back Button](#back_button_element) then it shifts back to Select Topics Page View.
- Label: **backButton**
  - he: '->'
  - en: '->'
- **The [Back Button](#back_button_element) visual element is already implemented and should be reused**

![back_button_mockup1](https://user-images.githubusercontent.com/12394551/74960880-cab30e00-5415-11ea-93a3-ba584c36da2f.png)
### 2.3.6. <a id="arguments_section_topic">Arguments Section</a>
- List of all suggestion arguments
- Sorted by creation time. Newer comes first according to the [Argument.created_at](../data_model.md#argument_created_at) field
- Each argument has 1 of 2 modes: Pro, Con according to the [Argument.type](../data_model.md#argument_type) field:
  - true - Pro (The pro argument should appear on green background)
  - false - Con (The con argument should appear on red background)
- Each argument is composed from 4 elements:
#### 2.3.6.1. <a id="argument_text_element">Argument Text</a>
[Argument contentHtml](../data_model.md#argument_contenthtml)
#### 2.3.6.2. <a id="user_avatar_element">User Avatar</a>
[Argument owner](../data_model.md#argument_owner)
#### 2.3.6.3. <a id="timestamp_element">Timestamp</a>
[Argument created_at](../data_model.md#argument_created_at)
#### 2.3.6.4. <a id="comments_list_element">Comments List</a>
Each comment is composed of 3 elements:
##### 2.3.6.4.1. <a id="comment_text_subelement">Comment Text</a>
[Comment contentHtml](../data_model.md#comment_contenthtml)
##### 2.3.6.4.2. <a id="user_avatar_subelement">User Avatar</a>
[Comment owner](../data_model.md#comment_owner)
##### 2.3.6.4.3. <a id="timestamp_subelement">Timestamp</a>
[Comment created_at](../data_model.md#comment_created_at)

![arguments_section_mockup1](https://user-images.githubusercontent.com/12394551/74990813-f4d3f280-544c-11ea-894a-2c3f48c6ef52.png)
- The [Arguments Section](#arguments_section_topic) logic and elements are already implemented in other existing page and **the code should be reused**
- see example in [here](https://new_votes_page.netlify.com/document/springfield/section?sectionById=269KTx7D1eVrbM0gTUM7&index=2)

![arguments_section_mockup2](https://user-images.githubusercontent.com/12394551/74990051-cfde8000-544a-11ea-8cd5-bb909db89874.png)
#### Overview:
- An argument corresponds to the Argument data-model
  - its 'sectionId' field links to the the section the argument relates to
  - A section may have multiple arguments
- A comment corresponds to the Comment data-model
  - its 'argumentId' field links to the the argument the comment relates to
  - its 'sectionId' field links to the the section the argument of the comment relates to
  - An argument may have multiple comments
### 2.3.7. <a id="get_notifications_check_boxes_topic">Get Notifications Check Boxes</a>
'New [Argument](../README.md#argument_definition) Or Comment' and 'New Edit Suggestion' Check boxes that allow the user to register for email notifications regards the current suggestion in the page.
- The user checks the Notification check boxes that he's interested getting email notifications
- The check box becomes marked/unmarked
- The corresponding [Section](../README.md#section_definition) data-model notifications field is updated
- Notification Types:
#### 2.3.7.1. <a id="new_argument_or_comment_element">New Argument Or Comment</a>
- Operation: Add/Remove current user id - [Section notifications newArgumentOrComment](../data_model.md#section_notifications_newargumentorcomment)
- Label: **newArgumentOrCommentNotification**
  - he: 'ברצוני לקבל עדכון כאשר מתווספים טיעון או הערה'
  - en: 'Get notification on new argument or comment'
#### 2.3.7.2. <a id="new_edit_suggestion_element">New Edit Suggestion</a>
- Operation: Add/Remove current user id - [Section notifications newEditSuggestionNotification](../data_model.md#section_notifications_neweditsuggestionnotification)
- Label: **newEditSuggestionNotification**
  - he: 'ברצוני לקבל עדכון כאשר מתווספת הצעה חדשה לשינוי הסעיף'
  - en: 'Get notification on new edit suggestions'

![get_notifications_check_boxes_mockup1](https://user-images.githubusercontent.com/12394551/75096605-eea75880-55a9-11ea-967d-1ead088dbd6f.png)
### 2.3.8. [_User Menu_](#user_menu_topic)
### 2.3.9. [_Bread Crumbs_](#bread_crumbs_topic)
## 2.4. <a id="summary_page">Summary Page</a>
This page is displayed once the user have finished voting on all Sections open for a vote.<br>
It gives the user feedback that she finished the task of voting,<br>
explain how she could continue participate in the process and encourage her to register for e-mail notifications for her choice
### 2.4.1. <a id="end_text_topic">End Text</a>
Static text, Edited by Admin user
### 2.4.2. <a id="notifications_panel_topic">Notifications Panel</a>
Displays all the notifications the user can register for:
- [Get Notification](../undefined/README.md#get_notifications_check_boxes_topic) for new document versions
- [Get Notification](../undefined/README.md#get_notifications_check_boxes_topic) for new edit suggestions
- [Get Notification](../undefined/README.md#get_notifications_check_boxes_topic) for new section suggestions
- [Get Notification](../undefined/README.md#get_notifications_check_boxes_topic) for new argument and comment
### 2.4.3. <a id="go_to_draft_button_topic">Go To Draft Button</a>
Change page view to [Draft](../README.md#draft_definition) page
- Label: **goToDraftButton**
  - he: 'לצפייה בטיוטת המסמך העדכנית'
  - en: 'View Updated Draft'
- Operation: Go to /document/[Document_id]/draft
### 2.4.4. [_User Menu_](#user_menu_topic)
### 2.4.5. [_Bread Crumbs_](#bread_crumbs_topic)
### Mockups

![summary_page_mockup1](https://user-images.githubusercontent.com/42510547/70627790-8219f000-1c2f-11ea-8b98-862679decad7.png)

![summary_page_mockup2](https://user-images.githubusercontent.com/12394551/71320197-a3d96980-24b0-11ea-9402-dbab60ab71b0.png)
## 2.5. <a id="draft_page">Draft Page</a>
The page goals are:
- Present overview of the [Document](../README.md#document_definition)
- Encourage the users to continue to suggestions page and participate in the discussion
- Let the user dive into details (sections, arguments, comments)
### 2.5.1. _Go to Suggestions Page_
### 2.5.2. _Sections Overview_
### 2.5.3. _Document Title_
### 2.5.4. _Document Menu_
### 2.5.5. [_User Menu_](#user_menu_topic)
# 3. <a id="topics">Topics</a>
## 3.1. <a id="user_menu_topic">User Menu</a>
High level [User](../README.md#user_definition) Navigation Panel
- Modes:
  - Desktop View: displayed always
  - Mobile View: side menu will displayed by clicking on side menu button
### 3.1.1. <a id="sign_out_element">Sign Out</a>
### 3.1.2. <a id="about_consenz_element">About Consenz</a>
### 3.1.3. <a id="about_this_document_element">About This Document</a>
### 3.1.4. <a id="go_to_draft_page_element">Go to Draft Page</a>
Clickable that directs the user to the [Draft Page](#draft_page)

The User Menu is already implemented in existing code. Need to integrate it also in new pages
## 3.2. <a id="bread_crumbs_topic">Bread Crumbs</a>
Breadcrumbs Navigation title that shows the relation to other pages in user flow for orientation
- [Bread Crumbs](#bread_crumbs_topic) should consist from:


    [document.id] - [section.topic] - [suggestionRelativePosition]
  - suggestionRelativePosition: **suggestionRelativePosition**
    - he: 'הצעה X מתוך Y'
    - en: 'suggestion X of Y'

for example, If the document id is **springfield**,<br>
the section topic is **אנרגיה**,<br>
the total suggestions is **12**<br>
and the current suggestion index is **2**<br>
then the [Bread Crumbs](#bread_crumbs_topic) should be:
- English: `springfield -> אנרגיה -> suggestion 2 of 12`
- Hebrew: `אנרגיה -> הצעה 2 מתוך 12 <- springfield`


**Breadcrumbs structure is already implemented. it should be integrated in new page**
## 3.3. <a id="user_avatar_topic">User Avatar</a>
[User](../README.md#user_definition) presentation (Name and icon).<br>
This presentation should also differ between a _regular_ user and _editor_ user.<br>
It is composed from 2 elements:
- [User](../README.md#user_definition) Name - String
- [User](../README.md#user_definition) Pic - Image
## 3.4. <a id="timestamp_topic">Timestamp</a>
Date of corresponding event (argument, comment, ect.),<br>
The [Timestamp](#timestamp_topic) element should present in 3 modes: _Published_, _Accepted_, _Declined_
