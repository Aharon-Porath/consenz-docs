# <a id="top">Consenz Navigation Project</a>
The details and mock ups of the different features that have to be developed
- [1. Features](#features)
  - [1.1. Navigation Tree](#navigation_tree)
    - [1.1.1. Visual](#visual_topic)
    - [1.1.2. Languages](#languages_topic)
    - [1.1.3. Actions](#actions_topic)
  - [1.2. Section Removal](#section_removal)
    - [1.2.1. Voting Logic](#voting_logic_topic)
    - [1.2.2. Pop-up](#pop-up_topic)
    - [1.2.3. Visual](#visual_topic)
  - [1.3. Related Sections Sorting Navigation Flow](#related_sections_sorting_navigation_flow)
- [2. Topics](#topics)
  - [2.1. Edit Section Suggestion Feed](#edit_section_suggestion_feed_topic)
  - [2.2. User Menu](#user_menu_topic)

# 1. <a id="features">Features</a>
## 1.1. <a id="navigation_tree">Navigation Tree</a>
The goal is to build a visual map<br>
to give the user an easy way to navigate between different parts of the [Document](../README.md#document_definition)<br>
and understand how the current page relates to the other pages.
### 1.1.1. <a id="visual_topic">Visual</a>
An hierarchical tree made of 4 levels:


    - Document Title
     - Topics Title
      - Sections of topic, In 2 Modes:
        1. {length} Sections Approved. 
          - Section Edit Suggestions
        2. {length} Sections in Discussion. 
          - Section Edit Suggestions
- By default the document title and topics title are visible
- [Section](../README.md#section_definition) Approved = sections of status 1
- [Section](../README.md#section_definition) in [Discussion](../README.md#discussion_definition) = sections of status 0, 4 and 7
#### 1.1.1.1. <a id="highlighted_path_element">Highlighted Path</a>
Elements of navigation tree that are part of the page current section path<br>
should be highlighted by bold fonts or by background color

For example, If the user is in a single section page of edit suggestion for section 2 of topic 3,<br>
then the elements that will be highlighted are:<br>
[Document](../README.md#document_definition) title> [Topic](../README.md#topic_definition) 3 title> section approve>, section 2> edit suggestion 1

#### 1.1.1.2. <a id="position_element">Position</a>
- In [User Menu](../VotingPage/README.md#user_menu_topic)

![position_mockup1](https://user-images.githubusercontent.com/55399150/80138047-e325dd00-85ac-11ea-940a-6b425ee0da94.png)
### 1.1.2. <a id="languages_topic">Languages</a>
- English: Navigation tree will be aligned in Left-to-Right direction

![comment_1_mockup1](https://user-images.githubusercontent.com/12394551/80029300-45200d00-84ef-11ea-9fd7-25ca9388dc4b.png)
- Hebrew: Navigation tree will be aligned in Right-to-Left direction

![comment_2_mockup1](https://user-images.githubusercontent.com/55399150/80139851-cb038d00-85af-11ea-840d-32422bbf5dac.png)
### 1.1.3. <a id="actions_topic">Actions (Behavior)</a>
- Clicking on element in the navigation panel does not changes the navigation flow (next, previous buttons), it's stay as is according to value in document sortBy
- Navigation element should show only item type and number (סעיף 2)
#### 1.1.3.1. <a id="document_title_element">Document Title</a>
- [User](../README.md#user_definition) Clicks on a [Document Title](#document_title_element) in the navigation tree
- Page view shifts to [Draft Page](../VotingPage/README.md#draft_page)
- [Navigation Tree](../VotingPage/README.md#navigation_tree_element) shows topics list under the document title.<br>
Each of the topics are collapsed so the sections under it are not shown
#### 1.1.3.2. <a id="topics_title_element">Topics Title</a>
- [User](../README.md#user_definition) Clicks on a [Topic Title](../VotingPage/README.md#topic_title_topic) in the navigation tree
- Page view shifts to [Topic](../README.md#topic_definition) [Voting Page](../VotingPage/README.md#voting_page)
- [Navigation Tree](../VotingPage/README.md#navigation_tree_element) shows approved topic [Section](../README.md#section_definition) list title and section edit suggestions list title.<br>
Each of the lists are collapsed so the suggestions under it are not shown
#### 1.1.3.3. <a id="topic_sections_in_discussion_element">Topic Sections in Discussion</a>
- [User](../README.md#user_definition) Clicks on a [Topic Sections in Discussion](#topic_sections_in_discussion_element) list in the navigation tree
- Page view shifts to
  - [Voting Page](../VotingPage/README.md#voting_page) (as when user clicks on topic sections counter of choostopics page or draft page)
  - single section page (a unique page for section, outside of vote pages/edit feed)
  - TODO does it has any difference from the case the user clicks on topic title - ?
- [Navigation Tree](../VotingPage/README.md#navigation_tree_element) shows the whole path to that section
  - Other sub trees, including approved topic sections list, are collapsed and do not show their inner items
#### 1.1.3.4. <a id="approved_topic_section_element">Approved Topic Section</a>
- [User](../README.md#user_definition) Clicks on a [Topic](../README.md#topic_definition) [Section](../README.md#section_definition) in the Approved [Section](../data_model.md#section) list in the navigation tree
- Page view shifts to draft page, and scroll to [Topic Title](../VotingPage/README.md#topic_title_topic) in draft page
- [Navigation Tree](../VotingPage/README.md#navigation_tree_element) shows the whole path to that section
  - Other sub trees, including topic sections in discussion list, are collapsed and do not show their inner items
#### 1.1.3.5. <a id="section_edit_suggestions_element">Section Edit Suggestions</a>
- [User](../README.md#user_definition) Clicks on a Suggestions of a [Section](../README.md#section_definition) in the navigation tree
- Page view shifts to [Edit Section Suggestion Feed](#edit_section_suggestion_feed_topic)
- [Navigation Tree](../VotingPage/README.md#navigation_tree_element) shows the [Section Edit Suggestions](#section_edit_suggestions_element) list title and its sections
  - Other sub trees are collapsed and do not show their inner items
#### 1.1.3.6. <a id="specific_section_edit_suggestion_element">Specific Section Edit Suggestion</a>
- [User](../README.md#user_definition) Clicks on a specific section edit suggestion in the navigation tree
- Page view shifts to [Edit Section Suggestion Feed](#edit_section_suggestion_feed_topic)
- [Navigation Tree](../VotingPage/README.md#navigation_tree_element) shows the whole path to that suggestion
  - Other sub trees are collapsed and do not show their inner items

![actions_mockup1](https://user-images.githubusercontent.com/55399150/80286630-36c33280-8735-11ea-83b7-72c06b1070ba.png)
## 1.2. <a id="section_removal">Section Removal</a>
Enable a way to remove a section from draft
- Apply the same logic and process in adding a section or an edit suggestion to draft.<br>
See full description [here](../logics.md#section_removed)
### 1.2.1. <a id="voting_logic_topic">Voting Logic</a>
- Approved Sections ([status](../data_model.md#section_status) is 1 or 5)
- Voting buttons remain active
- Apply [Section Removed](../logics.md#section_removed) logic
### 1.2.2. <a id="pop-up_topic">Pop-up</a>
In case a section is removed due to user voting than a pop-up is shown.<br>
(same as when a section in discussion reach threshold and approved)
- Label: **removedSectionPopup**
  - he: 'הסעיף נמחק! לצפייה בטיוטת המסמך העדכנית'
  - en: 'Section has been deleted! Click to see updated draft'

![pop_up_mockup1](https://user-images.githubusercontent.com/55399150/80315133-5e320200-87fe-11ea-86e8-a6fbf26e01aa.png)
### 1.2.3. <a id="visual_topic">Visual</a>
Besides to pop-up scenario, this page is shown in history page of section
- Navbar title of a removed section single page
  - Label: **removedSectionTitle**
    - he: 'סעיף שבוטל'
    - en: 'Deleted Section'
- Removed [Section](../README.md#section_definition) Time
  - Add section.deleted.at field to section data model
  - Label: **removedSectionInfo**
    - he: 'בוטל ב < deletion timestamp>'
    - en: 'Deleted At <deletion timestamp>'
- [Section](../README.md#section_definition) Info
  - [Topic](../README.md#topic_definition), Content, [User Avatar](../VotingPage/README.md#user_avatar_topic), ?? Voting Buttons ?? TODO fill me

![visual_mockup1](https://user-images.githubusercontent.com/55399150/80314302-650a4600-87f9-11ea-8a22-c9b039d598e6.png)
## 1.3. <a id="related_sections_sorting_navigation_flow">Related Sections Sorting Navigation Flow</a>
Apply [Related Sections](../logics.md#related_sections) logic<br>
Related Sections shows in edit section suggestions feed.<br>
[User](../README.md#user_definition) get to edit section suggestions in two ways:
1. By clicking on edit suggestions counter in section page, or
2. by clicking on section text in draft page
- In edit section suggestions feed page sort from top to button by the most agreed upon - show on top the section that their threshold is the smallest

# 2. <a id="topics">Topics</a>
## 2.1. <a id="edit_section_suggestion_feed_topic">Edit Section Suggestion Feed</a>
## 2.2. <a id="user_menu_topic">User Menu</a>
See [User Menu](../VotingPage/README.md#user_menu_topic)<br> 
The following should be added:
### 2.2.1. <a id="navigation_tree_element">Navigation Tree</a>
##### Feature: [Navigation Tree](../VotingPage/README.md#navigation_tree_element)
