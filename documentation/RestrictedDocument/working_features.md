
# <a id="top">Working Features</a>
Exiting Features, should work as described, straight after installation.

# 0.1 <a id="side-menu">Side-Menu</a>

Note: appear at all pages.

## Actions:

### 0.1.1 [Login / Sign out](#login-window)
### 0.1.2 Go to "About Consenz" page
### 0.1.3 Go to "About Document" page
### 0.1.4 Go to ["Draft"](#draft) page

![image](https://user-images.githubusercontent.com/5900841/89282163-cee58780-d653-11ea-98ea-1f002a5485ed.png)

# 0.2 <a id ="login-window">Login window pop-up</a>
Will open when user click on login button of side-menu, or when user tryes to interacte before login, i.e: Vote, add comment, add a new section, add a new edit section suggestion.
## 0.2.1 Login/sign up with google button
## 0.2.2 Go to sign up using email option
## 0.2.3 see terms page
sign up using email option:
## 0.2.4 Insert user name
## 0.2.5 Insert user email address
## 0.2.6 Insert new password
## 0.2.7 Go to login with email
Email login window:
## 0.2.8 Insert user email
## 0.2.9 Insert user password
## 0.2.10 Go to restore password
restore password window:
## 0.2.11 Insret user email

![image](https://user-images.githubusercontent.com/5900841/89527901-ca0b0a00-d7f2-11ea-840c-ecaca781ee8c.png)

# 1. <a id="welcome">Welcome page</a>

## Actions:

### 1.0 Open [Side-Menu](#side-menu)
### 1.1 Go to [Draft](#draft) button
### 1.2 Go to [Choose-Topics](#Choose-Topics) button

![image](https://user-images.githubusercontent.com/5900841/89281968-8201b100-d653-11ea-86aa-299d96d4eb2d.png)

# 2. <a id="choose-topics">Choose-Topics page</a>

## Actions:

### 2.0 Open [Side-Menu](#side-menu)
### 2.1 Breadcrumbs - go to [Welcome](#welcome) page
### 2.2 Breadcrumbs - go to [Draft](#draft) page
### 2.3 Go to Topic [Vote-Pages](#Vote-Page)
### 2.4 Go to General [Vote-Pages](#Vote-Page)

![image](https://user-images.githubusercontent.com/5900841/89294064-9b145d00-d667-11ea-9f4d-c06a4fa78d05.png)

# 3. <a id="Vote-Page"> Vote page</a>

## 3.1 <a id="vote-page-default-mode">Default Mode</a>

## Actions:

### 3.1.0 Open [Side-Menu](#side-menu)
### 3.1.1 Breadcrumbs - go to [Welcome](#welcome) page
### 3.1.2 Breadcrumbs - go to [Choose-topics](#Choose-Topics) page
### 3.1.3 Breadcrumbs - go to [Draft](#draft) page
### 3.1.4 Next button - Go to next [Vote-Page](#vote-page)
### 3.1.5 Back button - Go to last page visited

![image](https://user-images.githubusercontent.com/5900841/89295121-30fcb780-d669-11ea-9b78-ff2c1e07d5f5.png)

### 3.1.6 <a id="Vote-pro">Vote-pro</a>
#### 3.1.6.1 pro voting button change color
#### 3.1.6.2 counter on button add 1
#### 3.1.6.3 counter on "supporters needed" reduce 1:
![image](https://user-images.githubusercontent.com/5900841/89380818-dd3dad00-d700-11ea-9691-c417f9978eb6.png)
#### 3.1.6.4 If after voting pro "supporters needed" == 0, then:
1. "supporters needed" counter will disappear
2. Snackbar announcment "suggestion accepted" will showed
3. Click on the link on snackbar will load draft page
4. Section content will be added as a new card to [draft](#draft) page
![image](https://user-images.githubusercontent.com/5900841/89526468-7b5c7080-d7f0-11ea-9bad-39e4848a82e0.png)

### 3.1.7 Vote con
#### 3.1.7.1 con voting button change color
#### 3.1.7.2 counter on button add 1
#### 3.1.7.3 counter on "supporters needed" add 1
#### 3.1.7.4 ["add new edit section suggestion"](#Add-new-edit-section-suggestion) button appear
![image](https://user-images.githubusercontent.com/5900841/89381065-445b6180-d701-11ea-99d0-8fce2ceab7a4.png)

## 3.2 <a id="Vote-Page-Section-Edit-Suggestions-Tab-Mode">Section Edit Suggestions Tab Mode</a>
## Actions
### 3.2.1 Click on Edit Section Suggestions Tab
Display edit section suggestions list
### 3.2.2 "Show Changes" switch
True by default, after click cancel diff view of text
### 3.2.3 Show Comments list

![image](https://user-images.githubusercontent.com/5900841/89383369-052f0f80-d705-11ea-9fc0-75f9fbd0409d.png)
### 3.2.4 Vote on edit section suggestion
Should behave as [vote on section](#Vote-pro)
### 3.2.5 <a id="Add-new-edit-section-suggestion"> Add new edit section suggestion</a> button
### 3.2.6 Insert section content
### 3.2.7 Click Publish
A new section will be added, and the new section page should be loaded.
In data model, the section.parentSection field should get sectionId of the section which the user visit when publish the new edit section.
In parent section counter, edit section suggestions tab will add 1.
Also the new section ID should add to section.toEdit field of the parent section.
(Note: All publish buttons (for a new comment, comment on comment and sections) are greyd and in-active as long as text box is empty. Only after user insert text publish button became active)

![image](https://user-images.githubusercontent.com/5900841/89524015-7c8b9e80-d7ec-11ea-8d4d-cd78e2521588.png)

## 3.3 <a id="add_comments_mode"> Add Comments Mode </a>
## Actions
### 3.3.1 Add new comment button
Comment text box sould open
### 3.3.2 Insert comment content
### 3.3.3 Click "publish" button
New comment should be added to comments list, and the page view scroll to the new comment

![image](https://user-images.githubusercontent.com/5900841/89383719-a74ef780-d705-11ea-8b61-bb959c0ff5b7.png)

### 3.3.4 Add new comment on comment button
### 3.3.5 Insert comment on comment content
### 3.3.6 Click "publish" button
New comment on comment is added to list, and the page view scroll to the new comment on comment.

![image](https://user-images.githubusercontent.com/5900841/89530665-91216400-d7f7-11ea-994c-23dac67eb968.png)

## 3.4 <a id="last_page_mode">Last Page Mode</a>

## Actions:

### 3.4.1 [Add New Section](#add-new-section) Button
### 3.4.1 Go to [Summary](#Summary) Page

![image](https://user-images.githubusercontent.com/5900841/89295077-1aeef700-d669-11ea-8d44-f3a64b67e084.png)

# 4. <a id="summary-page"> Summary page</a>

## Actions:

### 4.0 Open [Side-Menu](#side-menu)
### 4.1 Breadcrumbs - go to [Welcome](#welcome) page
### 4.2 Breadcrumbs - go to [Draft](#draft) page
### 4.3 Notifications Check Box - 
Click mark check box
### 4.4 Go to [Choose-topics](#Choose-Topics) button
### 4.5 Go to [Draft](#draft) button
![image](https://user-images.githubusercontent.com/5900841/89418901-5c4ed780-d739-11ea-9f3b-cdbadb7b06da.png)

# 5. <a id="draft"> Draft Page</a>

## Actions:

### 5.0 Open [Side-Menu](#side-menu)
### 5.1 Go to Topic [Vote-Pages](#Vote-Page)
### 5.2 If there are edit suggestion for section: Go to [Section-Edit-Suggestions](#section_edit_suggestions) Page
### 5.2 If there are no edit suggestion for section: Go to [Section-History](#Section-History) Page
### 5.3 Open [Section-Side-Menu](#Section-Side-Menu)
#### 5.3.1 Go to [Section-Edit-Suggestions](#section_edit_suggestions) Page
#### 5.3.2 Go to [Section-History](#Section-History) Page
#### 5.3.3 Go to ["Add new edit section suggestion"](#Add-new-edit-section-suggestion) Page

![image](https://user-images.githubusercontent.com/5900841/89530209-cda09000-d7f6-11ea-9d40-ab0f8d2f236d.png)

### 5.4 Go to [Choose-topics](#Choose-Topics) button
### 5.5 [Add New Section](#add-new-section) button
### 5.6 Vote on document buttons
After click vote pro/con on document, change button color and counter should add 1. If click again, counter reduce 1. If click pro/con and then click con/pro, first button should reduce 1 and second button should add 1

![image](https://user-images.githubusercontent.com/5900841/89529538-97aedc00-d7f5-11ea-9b29-70a62de0277d.png)

# 6. <a id="section_edit_suggestions"> Section Edit Suggestions Page</a>.

## Actions:

## 6.1 [Vote pro/con](#Vote-pro)
## 6.2 Go to [section page](#Vote-Page)
## 6.3 [Add new edit section suggestion](#Add-new-edit-section-suggestion) button

![image](https://user-images.githubusercontent.com/5900841/89528397-a1374480-d7f3-11ea-995f-0f9d0ae504a5.png)

# 7. <a id="add-new-section"> Add New Section Suggestion Page </a>
## 7.1 Choose section topic dropdown
## 7.2 Insert section content text box
## 7.3 Publish button
After publish load new section vote page

![image](https://user-images.githubusercontent.com/5900841/89528937-8dd8a900-d7f4-11ea-8036-6912b74497c8.png)

# 8. <a id="history-page"> Section History Page </a>
## 8.1 [Vote pro/con](#Vote-pro)
## 8.2 [Add New Comment](#Add-Comments-Mode) button
## 8.2 [Add new edit section suggestion](#Add-new-edit-section-suggestion) button

![image](https://user-images.githubusercontent.com/5900841/89529941-4c48fd80-d7f6-11ea-8b45-cdf1938ec296.png)



