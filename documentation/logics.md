The logical specifications that are used in the pages flows
- [Suggestion Accepted](#suggestion_accepted)
- [Section Changed](#section_changed)
- [Section Removed](#section_removed)
- [Consensus Meter](#consensus_meter)
- [Most Agreed Upon](#most_agreed_upon)
- [User Connected Rule](#user-connected-rule)

# 1. <a id="suggestion_accepted">__Suggestion Accepted__</a>
A [Suggestion](./README.md/#suggestion_definition) on a [vote](./README.md/#vote_definition), i.e. its [status](./data_model.md/#status) is 0, 4 or 7, is considered 'Accepted' (or 'approved') when the difference between [pro](./data_model.md/#section_pros) votes count and [con](./data_model.md/#section_cons) votes count reaches the document [threshold](./data_model.md/#threshold) so that section threshold reach 0.

    suggestion.pros - suggestion.cons = document.threshold
    =>  suggestion Accepted
When suggestion is accepted it is added to [draft](./README.md/#draft_definition) page and its [status](./data_model.md/#status) changes:
- 0 => 1
- 4 => 1
- 7 => 1
# 2. <a id="section_changed">__Section Changed__</a>
A [Section](./README.md/#section_definition) that was already approved, i.e. its [status](./data_model.md/#status) is 1, is considered 'changed' when child section of it (i.e, another section that it's id is in toEdit field of the changed section) is accepted.  

When section is changed: 
1. Its [status](./data_model.md/#status) changes:
- 1 => 5
2. It will not displayed anymore at [draft](./README.md/#draft_definition) page.
3. It's child section will replace it - i.e. will displayed at it's position (topic and sarial number) at draft page.
4. It will be added to history page. 

## Notes
- Child section that have been accepted became parent section for all other sections related to changed section (i.e., all other section in toEdit field of changed section, and the changed section itself) and they will denoted by the inEdit field of the new parent section.

# 3. <a id="section_removed">__Expected: Section Removed__
A [Section](./README.md/#section_definition) that was already approved, i.e. its [status](./data_model.md/#status) is 1, is considered 'Removed' when the difference between [con](./data_model.md/#section_cons) votes count and [pro](./data_model.md/#section_pros) votes count = the document [threshold](./data_model.md/#threshold), so that section threshold reach 0.

- The logic of [Consensus Meter](#consensus_meter) will apply in case of deletion of a section the same as in approving section

When section is removed: 
1. Its [status](./data_model.md/#status) changes:
- 1 => 5
2. It will not displayed anymore at [draft](./README.md/#draft_definition) page.
3. If later a child section of the removed section will be approved, it will replace the removed section position, and the removed section will be added to history page. 

# 4 <a id="consensus_meter">__Consensus Meter__</a>
Every time thet a section is accepted (Expected: or removed), a new section_consensus_meter is added to consensuses field.

The value of the section_consensus_meter is calculated according to votes count on the section that have been accepted or removed as follows:

For section accepted:
- new consensuses item = (1 - ([con](./data_model.md/#section_cons) votes count /  [pro](./data_model.md/#section_pros) votes count)) * ([pro](./data_model.md/#section_pros)) / document users count)

Expected: For section removed:
- new consensuses item = (1 - ([pro](./data_model.md/#section_pros) votes count /  [con](./data_model.md/#section_cons) votes count)) * ([con](./data_model.md/#section_pros) / document users count)

Every time a new section_consensus_meter is created, document_consensus_meter is updated. 
The value of the new document_consensus_meter is calculated according to all section_consensus_meter average.

Every time the document_consensus_meter is updated, document_threshold is updated.
The value of document_threshold is document_consensus_meter * document users count.

document updated threshold will apply on all sections that are up to vote, and on new section suggestions and edit section suggestions that will be added by users.

## 4.1 Variables:
- consensusesArray: sections_consenus_meter
- x: the removed/acceppted section
- sectionDocumentId: the id of the [document](./README.md/#document_definition) the removed section relates to
- usersCount: the document users count
- consensusMeterAverage: sum of all sections_consenus_meter / sections of status 1 + 5 count

     
    sectionConsensus = (1 - (x.pros / x.cons)) * ((x.cons) / usersCount)
      Add sectionConsensus to consensusesArray
      Add sectionConsensus to consensusMeterAverage
    
    newThreshold = consensusMeterAverage * usersCount
      Apply newThreshold to all sections in discusstion and new sections as well:
        let be a section which its documentId is sectionDocumentId, than
        s.threshold = newThreshold
      Apply newThreshold to new sections in the document.

# 5. <a id="most_agreed_upon">__Most Agreed Upon__</a> Sorting
Sorting Algorithm that prefers suggestions that are closer to be accepted.<br>
i.e. Their threshold distance is closer to 0

## 5.1 Variables:
- threshold: data-model: Section, field: 'threshold'
- prosConsDelta: Section.pros.length() - Section.cons.length()
- thresholdDistance: threshold - prosConsDelta = threshold + Section.cons - Section.pros
- suggestionsList: List of all [Suggestions](./README.md/#suggestion_definition) for voting according to user selection in the Choose Topics page. The list should consist of all [Section](./data_model.md/#section) instances which their [status](./data_model.md/#status) field is 0 or 4 and that their 'topic' field belongs to a topic that the user selected in the Choose Topics page.
- x, y: Suggestion items in suggestionsList for voting

## 5.2 Rules
- The algorithm works on section with status 0, 4 or 7.<br>
  A section with larger prosConsDelta is sorted higher
- If prosConsDelta of two sections equal, sort them according to section createdAt,<br>
  from late to early (the later is sorted higher)
- Section of status 1 are sorted lowest (in the end of the list).
- the order of sections with status 1 is by acceptance timestamp.<br>
  (The later accepted section sorted higher)

## 5.3 Logic:
    For x, y in suggestionsList:
    x before y if thresholdDistance of x is smaller than thresholdDistance of y.
    I.e. x before y if (x.threshold - (x.pros - x.cons)) < (y.threshold - (y.pros - y.cons))
    I.e. x before y if (x.threshold + x.cons - x.pros) < (y.threshold + y.cons - y.pros)
    
    * If 2 or more suggestions have the same thresholdDistance, than the sorting
    would prefer (show first) the newer suggestion according to the Section.created_at field.

# 6. Navigation Rules
## 6.1. <a id="related-sections">__Related Sections__</a>
Sections that have parent-child relations
- "child" is section that it's id is in toEdit field of another section
- "parent" is a section that it'd id is in parentSection of another section
- parent may have multiple child sections.
- child may have only one parent section.

| Section   |      Id   |      toEdit   |      parentSectionId   |      prosConsDelta
|----------|:-------------:|:-------------:|:-------------:|:-------------:|
| A (Parent) | 0000a | 0000b,0000c | | 1
| B (Child of A) | 0000b |  | 0000a | 2
| C (Child of A) | 0000c |  | 0000a | 3

### 6.1.1. <a id="relation-group">Relation Group</a>
A group of sections that are related to each other.<br>
In the above example A,B,C are all belong to the same Relation Group
### 6.1.2. <a id="relation-group-root-section">Relation Group Root Section</a>
The root parent of the sections in the group.<br>
In the example A is the group root section
### 6.1.3. <a id="relation-group-agent">Relation Group Agent</a>
The section agent of this group. this section represents the group in the navigation flow.<br>
The picked agent is according to this rules:
- Section is up for voting (status 0,4 or 7)
  - The section has the highest prosConsDelta (pro votes minus con votes) in the group
  - In case two sections have the same prosConsDelta value,<br>
  pick the newer suggestion (according to the Section.created_at field).
- If there is no section up for voting, pick the approved section (status 1)
  - There can be only one section of status 1 in a relation group.<br>
  If another section in the relation group change its status to 'approved' (1)<br>
  then the previous approved section changes it stauts to 5).
#### Note
If due to user voting, another section in the relation group reaches the highest prosConsDelta value, than it should become the agent of the group

## 6.2. <a id="attached-relation-groups">__Attached Relation Groups__</a>
A [relation group](#relation-group) may be attached to another relation group in uni-directional way.
- The relation is determined by the 'attachedTo' field of the [relation group root section](#relation-group-root-section)
- The [relation group agent](#relation-group-agent) inherits the attached relation group of the root section 

We can say that "A is attached to D" if
- A is the agent of relation group X
- D is the agent of relation group Y
- Relation group X is attached to Relation group Y
### 6.2.1. <a id="attached-sections-rule">__Attached Sections Rule__</a>
If Section Agent A is attached to Section Agent D<br>
Then section D should always follow section A in the vote pages navigation.

    A -> D
- Even if D had higher prosConsDelta than A, it would still follow Section A.
- If sections A or D are approved they should still show next to each other in the flow
### 6.2.2. <a id="attachment-change-rule">Attachment Change Rule</a>
A change in prosConsDelta of [related section](#related-sections)<br>
may change the [relation group agent](#relation-group-agent) and lead to a change in navigation flow<br>
Following the previous definition, if B is an Edit Suggestion of section A (B child of A)<br>
and due to user voting B prosConsDelta value get higher than A so:<br>
B becomes the [agent](#relation-group-agent) of the group and inherits the attachment to D

    B -> D
### 6.2.3. <a id="attachment-chain">Attachment Chain</a>
If A is attached to D and D is attached to E, they compose an Attachment Chain

    A -> D -> E
### 6.2.4. <a id="attachment-chain-head">Attachment Chain Head</a>
The first section in the attachment chain (A)
- The [Most Agreed Upon](#most_agreed_upon) algorithm apply on the head section of attachment chain, in this case section A, so the prosConsDelta value of section A is the one processed in the soring logic
## 6.3. Sorting Algorithm
Given a group of sections, compose an ordered sub list of sections to show in the navigation flow
1. Transform the group of sections into a list of relation groups [agents](#relation-group-agent)
2. Transform the list of agents into a list of [attachment chains](#attachment-chain)
3. Apply the [Most Agreed Upon](#most_agreed_upon) algorithm on the [heads](#attachment-chain-head) of the chains list, ang get an ordered head sections list.
4. Apply the [Attached Sections Rule](#attached-sections-rule) to transform the ordered head list into the navigation flow
### Example
- A is parent of B and C (A,B,C belong to the same relation group which its root section is A)
- D is parent of F
- A is attached to D (A.attachedTo = D.id)
- D is attached to E.
- G and H are not attached and not related to other sections

| Section   |      Id   |      status   |      prosConsDelta   |      toEdit   |      parentSectionId|      attachedTo
|----------|:-------------:|:-------------:|:-------------:|:-------------:|:-------------:|:-------------:|
| A | 0000a | 0 | 2 | 0000b,0000c |  | 0000d
| B | 0000b | 7 | 5 |  | 0000a
| C | 0000c | 7 | 1 |  | 0000a
| D | 0000d | 0 | 4 | 0000f |  | 0000e
| E | 0000e | 0 | 1 |  |  | 
| F | 0000f | 7 | 2 |  | 0000d
| G | 0000g | 0 | 1 |  |  |
| H | 0000h | 0 | 7 |  |  | 

####1. Transform the group of sections into a list of relation groups agents
    B(,A,C)    D(,F)    E    G    H
- B has higher prosConsDelta than A and C, so B is the agent in the A,B,C relation group
- D has higher prosConsDelta than F, so D is the agent in the D,F relation group
####2. Transform the list of agents into a list of attachment chains
    B->D->E    G    H
- B inherits the attachment to D from A
####3. Apply the Most Agreed Upon algorithm on the heads of the chains list
    H(7)    B(5)    G(1)    
####4. Apply the Attached Sections Rule to transform the ordered head list into the navigation flow
    H B->D->E G
    =>
    H, B, D, E, G    

### Note:
The sorting order should be updated once when the page loads,<br>
to prevent page rendering while the user navigates in the vote pages

## 6.4. Navigation Examples
### Example 1
- A is parent of B and C (B,C are edit suggestions of A)
  - B has the highest prosConsDelta (8) 
  
| Section   |      Id   |      status   |      prosConsDelta   |      toEdit   |      parentSectionId|      attachedTo
|----------|:-------------:|:-------------:|:-------------:|:-------------:|:-------------:|:-------------:|
| A | 0000a | 0 | 4 | 0000b,0000c 
| B | 0000b | 7 | 8 |  | 0000a
| C | 0000c | 7 | 3 |  | 0000a
| D | 0000d | 0 | 2 |  |  | 
| E | 0000e | 0 | 6 |  |  | 
| F | 0000f | 0 | 7 |  |  | 
#### Expected Navigation Order
    B, F, E, D
  - The navigation order is according to prosConsDelta values only

### Example 2
| Section   |      Id   |      status   |      prosConsDelta   |      toEdit   |      parentSectionId|      attachedTo
|----------|:-------------:|:-------------:|:-------------:|:-------------:|:-------------:|:-------------:|
| A | 0000a | 1 | 5 | 0000b,0000c |  | 0000d
| B | 0000b | 4 | 4 |  | 0000a
| C | 0000c | 4 | 3 |  | 0000a
| D | 0000d | 0 | 2 |  |  | 0000e
| E | 0000e | 0 | 7 |  |  | 
- A is parent of B and C (B,C are edit suggestions of A)
  - A is approved (status 1), B has prosConsDelta value higher than C<br>
  so B is the [agent](#relation-group-agent) of the (A,B,C) relation group
- A is attached to D, B inherits this attachment
- D is attached to E
#### Expected Navigation Order
    B, D, E
- Even though E has the highest prosConsDelta value,<br>
  it is still shown after B and D, since this is the order determent by the attachment direction (B -> D , D -> E).

#### Note
If B gets approved, then the status of A changes to 5, and A does not return navigation flow.

### Example 3
- A is attached to D, D is attached to E
- A is parent of B and C (B,C are edit suggestions of A)
  - B is Accepted (stauts is 1)
  - A and C have equal prosConsDelta values
  - C was created after A (C.craetedAt > A.craetedAt)
- C becomes the [agent](#relation-group-agent) of the (A,B,C) relation group
  - C inherits the attachment to D from A 

| Section   |      Id   |      status   |      prosConsDelta   |      toEdit   |      parentSectionId|      attachedTo | craetedAt
|----------|:-------------:|:-------------:|:-------------:|:-------------:|:-------------:|:-------------:|:-------------:|
| A | 0000a | 0 | 3 | 0000b,0000c | | 0000d | 1.1.2020
| B | 0000b | 1 | 6 |  | 0000a
| C | 0000c | 4 | 3 |  | 0000a | | 2.1.2020
| D | 0000d | 0 | 2 |  |  | 0000e
| E | 0000e | 0 | 1 |  |  | 
#### Expected Navigation Order
    C, D, E

### Example 4
- A is attached to D, D is attached to E
- A is parent of B and C (B,C are edit suggestions of A)
  - B is the [agent](#relation-group-agent) of the (A,B,C) relation group since it has the highest prosConsDelta value (3)
- D is parent of H (H is an edit suggestion of D)
  - H has higher prosConsDelta value (6) than D (5) so H is the [agent](#relation-group-agent) of the D,H relation group
- F and G are not attached or related to other sections

| Section   |      Id   |      status   |      prosConsDelta   |      toEdit   |      parentSectionId|      attachedTo
|----------|:-------------:|:-------------:|:-------------:|:-------------:|:-------------:|:-------------:|
| A | 0000a | 0 | 2 | 0000b,0000c |  | 0000d 
| B | 0000b | 7 | 3 |  | 0000a
| C | 0000c | 7 | 2 |  | 0000a
| D | 0000d | 0 | 5 | 0000h |  | 0000e
| E | 0000e | 0 | 6 |  |  | 
| F | 0000f | 0 | 7 |  |  | 
| G | 0000g | 0 | 4 |  |  | 
| H | 0000h | 7 | 6 |  | 0000d | 

#### Expected Navigation Order
    F, G, B, H, E
- B,H,E come one after another since they all in the same [attachment chain](#attachment-chain)
  - B is a Child of A
  - H is a child of D
  - A is attached to D
  - D is attached to E
- F is first since it has the highest prosConsDelta value (7)
- G prosConsDelta value (4) is higher than B(3) the head of the B,H,E chain so G comes second, before that chain.<br>
  Even though G prosConsDelta value is lower than H(6) and E(6)

### Example 5
- A is attached to D, D is attached to E
- A is parent of B and C (B,C are edit suggestions of A)
  - B has the highest prosConsDelta (8)
- F is not attached to any section
  - F has the second highest prosConsDelta (7) after B

| Section   |      Id   |      status   |      prosConsDelta   |      toEdit   |      parentSectionId|      attachedTo
|----------|:-------------:|:-------------:|:-------------:|:-------------:|:-------------:|:-------------:|
| A | 0000a | 0 | 4 | 0000b,0000c |  | 0000d 
| B | 0000b | 7 | 8 |  | 0000a | 0000d
| C | 0000c | 7 | 3 |  | 0000a
| D | 0000d | 0 | 2 |  |  | 0000e
| E | 0000e | 0 | 6 |  |  | 
| F | 0000f | 0 | 7 |  |  | 
#### Expected Navigation Order
    B, D, E, F
    
### Example 6
- A is parent of B and C (B,C are edit suggestions of A)
  - B is the [agent](#relation-group-agent) in this relation group since it has the highest prosConsDelta (7) in the group
- D is attached to F

| Section   |      Id   |      status   |      prosConsDelta   |      toEdit   |      parentSectionId|      attachedTo
|----------|:-------------:|:-------------:|:-------------:|:-------------:|:-------------:|:-------------:|
| A | 0000a | 0 | 4 | 0000b,0000c 
| B | 0000b | 7 | 7 |  | 0000a
| C | 0000c | 7 | 3 |  | 0000a
| D | 0000d | 0 | 2 |  |  | 0000f
| E | 0000e | 0 | 6 |  |  | 
| F | 0000f | 0 | 8 |  |  | 
#### Expected Navigation Order
    B, E, D, F
- F follow D, although its prosConsDelta value is the highest (8)


- Illustration:
[image](https://user-images.githubusercontent.com/5900841/80367632-21184f00-8894-11ea-8497-b7fa525a7836.png)

# 7 <a id="user-connected-rule">__User Connected Rule__</a>
When the user tries to perform an action that only a Logged-In (Connected) user can perform.<br>
- If the user is connected than the action executes according to the action logic.<br>
- If the user is not connected, then he is directed to login page.<br>
After the user logs in, he is directed back to the page where the action he wanted to perform<br>
and the action continue to execute according to the action logic (feedback, to, ...)  
