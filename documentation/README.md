- [Project Overview](#project-overview)
- [Data Model](#data-model)
- [Logics](#logics)
- [Features](#features)
- [Road Map](#road_map)

# 1. <a id="project-overview">Project Overview</a>
A platform for creating agreements.<br>
The platform lets a group of people create a document that reflects the issues they agree upon<br>
and discuss the issues that are in disagreement.

The platform allows any group of people at any scale to formulate a text<br>
in a single, coherent and clear document in a transparent and democratic way.<br>
The platform enable it through a new kind of Internet discussion.<br>
Instead of spreading across countless responses,<br>
the discussion converges around a collaborative and democratic document<br>
by incorporating voting mechanisms with discussion tools.<br>
This allows to distinguish between agreed upon and controversial issues,<br>
and the process has a clear product: A text that reflects the consent of the participants.
## 1.1. <a id="technologies-overview"></a>Technologies
- Vue
- Vue-typescript
- Vuex-typescript
- Vuetify
- Firebase
- Vuex-easy-firestore
## 1.2. <a id="definitions">Definitions</a>
Terms and definitions of the application structure and components.
- <a id="document_definition">__Document__</a>: An object that covers all the relevant issues that the users have discussed, voted and agreed upon.<br>
  The Document is dynamic and change according to the actions of the users.
- <a id="topic_definition">__Topic__</a>: Sub part of the document.<br>
  A document may have multiple Topics.
- <a id="section_definition">__Section__</a>: One issue in the Topic.<br>
  a Topic may have multiple Sections.
- <a id="sub-section_definition">__Sub-Section__</a>: Sub part of a Section.<br>
  Sections may have multiple Sub-Sections.
- <a id="version_definition">__Version__</a>: Old stats of the Document.<br>
  A Document may have multiple Versions.
- <a id="draft_definition">__Draft__</a>: A state of a Document in a given time, i.e .<br>
  the most updated Version of the Document.<br>
  A Document can have only one draft.
- <a id="suggestion_definition">__Suggestion__</a>: A Section which is still in discussion and stand for a vote and discussion
- <a id="edit_suggestion_definition">__Edit Suggestion__</a>: A Suggestion that stands to replace another Section.<br>
  A Section may have multiple Edit Suggestions.
- <a id="argument_definition">__Argument__</a>: A statement regards a Suggestion.<br>
  An Argument can be either pro (for) or con (against) a Suggestion.<br>
  A Suggestion may have multiple Arguments
- <a id="comment_definition">__Comment__</a>: A note that represent an opinion of a user regarding an Suggestion.<br>
  a Suggestion may have multiple Comments
- <a id="comment_on_a_comment_definition">__Comment on a Comment__</a>: A note that represent an opinion of a user regarding a Comment.<br>
  a Comment may have multiple Comment on Comments
- <a id="discussion_definition">__Discussion__</a>: The sum of all Comments regards a Suggestion
- <a id="vote_definition">__Vote__</a>: A way for the users to express support or objection to a Suggestion without adding text.<br>
  A Vote can be pro or con.<br>
  A Suggestion may have multiple Votes.
- <a id="document_threshold_definition">__Document Threshold__</a>: A number that represent how much support needed to approve a new suggestion.<br>
  The threshold is always a percentage of the total sum of users in a document at given time
- <a id="suggestion_threshold_definition">__Suggestion Threshold__</a>: A number that calculate Document Threshold - Pro Voters{length} + Con Voters{length}.<br>
  When Suggestion Threshold reach 0 Section status changes to "approved".
- <a id="user_definition">__User__</a>: A member in the platform that may create a Section, vote in discussion, comment on an argument.<br>
  ect
- <a id="discussion_process_definition">__Discussion Process__</a>: The purposes and intentions of the initiator(s) of the process that include the issues that stand for discussion and the goals that the created document should fulfill.
# 2. <a id="data-model">Data Model</a>
- [User](./data_model.md#user)
- [Document](./data_model.md#document)
- [Section](./data_model.md#section)
- [Argument](./data_model.md#argument)
- [Comment](./data_model.md#comment)
- [ChangeEvent](./data_model.md#changeevent)
# 3. <a id="logics">Logics</a>
- [Suggestion Accepted](./logics.md#suggestion_accepted)
- [Section Changed](./logics.md#section_changed)
- [Section Removed](./logics.md#section_removed)
- [Consensus Meter](./logics.md#consensus_meter)
- [Most Agreed Upon](./logics.md#most_agreed_upon)
- [Navigation Rules](./logics.md#navigation_rules)
- [User Connected Rule](./logics.md#user_connected_rule)
- [Related Sections](./logics.md#related_sections)
# 4. <a id="features">Features</a>
- [Voting Page](VotingPage/README.md)
- [Restricted Document](RestrictedDocument/README.md)
# 5. <a id="road_map">Road Map</a>
- [Document Users List](DocumentUsersList/README.md)
- [Navigation Tree](NavigationTree/README.md)
- [Update Bell](UpdateBell/README.md)
