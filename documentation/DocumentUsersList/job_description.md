# 1. <a id="job_requirements">Job Requirements</a>
Testing system for Vue application and more features
## 1.1. Writing Tests
E2E Tests that Simulate a user browsing the application, voting, commenting and doing any operation
- The Freelancer should suggest a solution for E2E infrastructure that supports:
  - Automated Client side simulation
  - CICD integration with github actions
- Cover all [working features](./working_features.md)<br>
Each of the features should have its own test:
  - Side-Menu
  - Welcome Page
  - Choose-Topics
  - Default Mode Voting
  - Section Edit Suggestions Tab Mode Voting 
  - Add Comments Mode
  - Last Page Mode
  - [Summary Page](../VotingPage/README.md#summary_page)
  - Draft
  - Section Edit Suggestions
  - Add New Section Suggestion
  - Section History
## 1.2. New Features Specifications
- [Document Users List](./README.md#document_users_list)
- [Comments Feed](./README.md#comments_feed)
# 2. <a id="milestones">Milestones</a>
The total price will be split into 10 milestones, each for 10% of the payment.<br>
milestones 1-6 are dedicated for setting up a the testing infrastructure and supporting all known working features.<br>
milestones 7-10 are dedicated for developing the new features
1. Tests: [Side-Menu](./working_features.md#side-menu), [Welcome Page](./working_features.md#welcome) and [Choose-Topics](./working_features.md#choose-topics)
2. Tests: [Default Mode Voting](./working_features.md#vote-page-default-mode)
3. Tests: [Section Edit Suggestions Tab Mode Voting](./working_features.md#vote-page-default-mode)
4. Tests: [Add Comments Mode](./working_features.md#add_comments_mode), [Last Page Mode](./working_features.md#last_page_mode) and [Summary Page](./working_features.md#summary-page)
5. Tests: [Draft](./working_features.md#draft) and [Section Edit Suggestions](./working_features.md#section_edit_suggestions)
6. Tests: [Add New Section Suggestion](./working_features.md#add-new-section) and [Section History](./working_features.md#history-page) Tests
7. [Document Users List](./userStories/user_story.md#document_users_list_step)
8. [Comments Feed](./userStories/user_story.md#comments_feed_step)
9. [Clicking a Comment](./userStories/user_story.md#clicking_a_comment_step)
10. [Restricted Document](./userStories/user_story.md#restricted_document_step)
