# <a id="top">Document Users List</a>
Document User List, Comments Feed and Version Page
- [1. Pages](#pages)
  - [1.1. Document Users List](#document_users_list)
    - [1.1.2. Navigation](#document_users_list_navigation_property)
    - [1.1.2.1. Navbar Title](#navbar_title_topic)
    - [1.1.2.2. Users List](#users_list_topic)
    - [1.1.2.3. Navbar Back Button](#navbar_back_button_topic)
  - [1.2. Comments Feed](#comments_feed)
    - [1.2.2. Navigation](#comments_feed_navigation_property)
    - [1.2.2.1. Navbar Title](#navbar_title_topic)
    - [1.2.2.2. Sections with comments List](#sections_with_comments_list_topic)
  - [1.3. Versions Page](#versions_page)
    - [1.3.2. Navigation](#versions_page_navigation_property)
    - [1.3.2.1. Navbar Title](#navbar_title_topic)
    - [1.3.2.2. Approved Sections List](#approved_sections_list_topic)
    - [1.3.2.3. Navbar Back Button](#navbar_back_button_topic)

# 1. <a id="pages">Pages</a>
## 1.1. <a id="document_users_list">Document Users List</a>
A Page that shows all users that participate in a [Document](../README.md#document_definition) discussion
### 1.1.1. <a id="document_users_list_navigation_property">Navigation</a>
- In [Draft Page](../VotingPage/README.md#draft_page), The user clicks on the participants link.<br>
The [Document Users List](#document_users_list) page should appear

![navigation_mockup1](https://user-images.githubusercontent.com/5900841/81645444-42e80900-9432-11ea-8100-260593524db4.png)

TODO Fix Mockup, Main Navbar should not contain the back button
### 1.1.2. Topics
#### 1.1.2.1. <a id="navbar_title_topic">Navbar Title</a>
The title in the purple navigation panel
- Label: **usersListNavbarTitle**
  - he: 'משתתפים בדיון'
  - en: 'Participants'
#### 1.1.2.2. <a id="users_list_topic">Users List</a>
List of [User](../README.md#user_definition) info cards that are assigned to the document
##### 1.1.2.2.1. <a id="user_criteria_to_be_in_the_list_element">User Criteria to be in the list</a>


    return all Users that their User.documents contains document.id
##### 1.1.2.2.2. <a id="order_element">Order</a>
By [User.created_at](../data_model.md#user_created_at), From Latest to Earliest
##### 1.1.2.2.3. <a id="user_card_element">User Card</a>
###### 1.1.2.2.3.1. <a id="user_pic_subelement">User Pic</a>
###### 1.1.2.2.3.2. <a id="user_name_subelement">User Name</a>
- Font Size: 18
###### 1.1.2.2.3.3. <a id="user_joining_date_subelement">User Joining Date</a>
[User created_at](../data_model.md#user_created_at)
- Formatting: Only date, without hour and minutes
- Label: **userJoinedAt**
  - he: '-הצטרפ/ה ב {joinDate}'
  - en: 'Joined At {joinDate}'
#### 1.1.2.3. <a id="navbar_back_button_topic">Navbar Back Button</a>
- Navbar should contain a [Back Button](../VotingPage/README.md#back_button_element)
- Clicking on the back button should shift the page back to [Draft Page](../VotingPage/README.md#draft_page)

In page: - Keep showing document info counters as at top of draft page.<br>
Below users counter add under-line to signal the user which page he sees now.<br>
There should be a line separator between the user cards in the list

### 1.1.3 Implementation
- [UsersListPage.vue](https://github.com/wonderfloyd/Consenz/blob/master/src/views/Document/UsersListPage/UsersListPage.vue) is the view that displays all the users assigned to a specific document.
- In the `usersList` method the store's `UsersModule` is utilized to retrieve all users of the document from the DB, then sorted by desc order and returned.
- The date in each user's list item is formatted using `dateFormatted` from the store's [DisplayModule](https://github.com/wonderfloyd/Consenz/blob/master/src/store/modules/displayModule.ts).
- [NavBar.html](https://github.com/wonderfloyd/Consenz/blob/master/src/views/NavBar/NavBar.html) is rendering conditionally based on `isUsersListPage` from [NavBar.vue](https://github.com/wonderfloyd/Consenz/blob/master/src/views/NavBar/NavBar.vue) which is returning a boolean based on current route.
- In [router.ts](https://github.com/wonderfloyd/Consenz/blob/master/src/router.ts) a route named `usersList` is set.
## 1.2. <a id="comments_feed">Comments Feed</a>
A Page that shows all sections that have comments and arguments

![comments_feed_mockup1](https://user-images.githubusercontent.com/5900841/81648122-d7546a80-9436-11ea-81f4-a4a5606e2c54.png)

### 1.2.1. <a id="comments_feed_navigation_property">Navigation</a>
- In [Draft Page](../VotingPage/README.md#draft_page), The user clicks on the comments link.<br>
The [Comments Feed](#comments_feed) page should appear
### 1.2.2. Topics
#### 1.2.2.1. <a id="navbar_title_topic">Navbar Title</a>
The title in the purple navigation panel
- Label: **commentsFeedNavbarTitle**
  - he: 'תגובות לסעיפי המסמך'
  - en: 'Comments on Document Sections'
#### 1.2.2.2. <a id="sections_with_comments_list_topic">Sections with comments List</a>
List of [Section](../README.md#section_definition) cards that have comments and arguments
##### 1.2.2.2.1. <a id="sections_with_comments_list_filter_property">Filter</a>
Need to iterate over all document comments and arguments,<br>
check the sections they relate to (Comment.sectionId and arguments.sectionID)<br>
and compose a list from all those sections
##### 1.2.2.2.2. <a id="sections_with_comments_list_order_property">Order</a>
By Comment.created_at/arguments.created_at, From Latest to Earliest<br>
I.e A section that have a comment or argument that was added lately will show first

The section should retrieve its latest comment or argument creation time (a section may have multiple comments/arguments)<br>
and in this page is calculated only by the order rule

##### 1.2.2.2.3. <a id="section_card_element">Section Card</a>
A Card that shows information related to a section. It includes:
- Operation: On click a section single page should appear (outside voting flow),<br>
and the page view should scroll to the relevant comment
###### 1.2.2.2.3.1. <a id="topic_title_subelement">Topic title</a>
###### 1.2.2.2.3.2. <a id="section_content_subelement">Section Content</a>
###### 1.2.2.2.3.3. <a id="voting_buttons_subelement">Voting Buttons</a>
###### 1.2.2.2.3.4. <a id="comments_section_subelement">Comments Section</a>
###### 1.2.2.2.3.5. <a id="add_new_comment_button_subelement">Add New Comment Button</a>
- The components code and visuals are already implemented in Sections for vote list Page:<br>
https://consenz-te0.netlify.app/document/springfield/section?sectionsByStatus=0
- **The code should be reused**
## 1.3. <a id="versions_page">Versions Page</a>
A Page that shows all [Document](../README.md#document_definition) draft approved sections
### 1.3.1. <a id="versions_page_navigation_property">Navigation</a>
- In [Draft Page](../VotingPage/README.md#draft_page), The user clicks on the versions link.<br>
The [Versions Page](#versions_page) should appear.

![navigation_mockup1](https://user-images.githubusercontent.com/5900841/81670107-cbc16d80-944f-11ea-8acf-beb112be520a.png)
### 1.3.2. Topics
#### 1.3.2.1. <a id="navbar_title_topic">Navbar Title</a>
The title in the purple navigation panel
- Label: **versionsFeedNavbarTitle**
  - he: 'גרסאות קודמות למסמך'
  - en: 'Previous Document Versions'
#### 1.3.2.2. <a id="approved_sections_list_topic">Approved Sections List</a>
List of [Section](../README.md#section_definition) that were approved
- There should be a line separator between the sections in the list
##### 1.3.2.2.1. <a id="approved_sections_list_filter_property">Filter</a>
All Sections that:
- Section.documentId is the id of the Draft document
- Section.status is 1 or 5
##### 1.3.2.2.2. <a id="approved_sections_list_order_property">Order</a>
The sections will display by their order in draft,<br>
i.e by their serial number, from first to last.<br>
Serial number does not exist in data-model, need to find a way to take it from draft page

To section show all versions (i.e, toEdit/parentSection of status 1 or 5) sort by accepted at time, as in history page, But - without voting and comments buttons

A link for history page - https://consenz-master.netlify.app/document/springfield/section?sectionsByStatus=5&index=2&id=Aa8Ns7AxytAwoDnsV7Vd

##### 1.3.2.2.3. <a id="section_card_element">Section Card</a>
A Card that shows information related a section in the list. It includes:
- Operation: When the user clicks on the section content area<br>
page should shift to section history page
- Label: **versionSection**
  - he: 'גרסה X לסעיף Y'
  - en: 'Version X to Section Y'


    X = version number, Y = serial number of section in draft page.
    Version number determine by the acceptedAt date of the section,
    from early to late (already implemented in history page)
###### 1.3.2.2.3.1. <a id="topic_title_subelement">Topic title</a>
###### 1.3.2.2.3.2. <a id="section_content_subelement">Section Content</a>
#### 1.3.2.3. <a id="navbar_back_button_topic">Navbar Back Button</a>
- Navbar should contain a [Back Button](../VotingPage/README.md#back_button_element)
- Clicking on the back button should shift the page back to [Draft Page](../VotingPage/README.md#draft_page)
