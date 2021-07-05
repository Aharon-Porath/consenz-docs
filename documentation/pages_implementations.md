<h1><a id="top">Consenz Pages and Flows Implementations</a></h1>

The details about the actual technology implementations of the different pages and flows.
- [Draft](#draft)
- [Draft To Sections](#draft-to-sections)
  
# 1. <a id="draft">Draft</a>
A Page that presents a Document [Draft](./README.md/#draft_definition)
- Source: Draft.ts
![Image20191216104624](https://user-images.githubusercontent.com/12394551/70894763-56638500-1ff6-11ea-8983-ff8c72d76ef2.png)
## 1.1. <a id="draft-highlighted">Highlighted</a>
    @storeHelper.SectionsModule.SectionsGetter
    private sectionsByStatus: (number, string) => ParentSectionInterface[];
    
    get sections()
    this.sectionsByStatus(enums.SECTION_STATUS.approved, this.initialParentId);
## 1.2. <a id="router">Router</a>
- Source: router.ts
- Path: /document/:prettyLink/draft
- Name: draft
- Component: Draft
## 1.3. Store
## 1.3.1. Main Module
- Source: store/modules/mainModule.ts
##### Highlighted
    preetyLink
    initStore()
## 1.3.2. Helper
- Source: store/store.helper.ts
##### Highlighted
    MainModule
    SectionsModule
## 1.3.2. Sections
- Source: store/modules/sectionsModule.ts
##### Highlighted
    allSections
    sectionsByStatus
## 1.3.3. Router Module
- Source: store/modules/routerModule.ts
##### Highlighted
    setToState

# 2. <a id="draft-to-sections">Draft To Sections</a>
Draft to Sections Page Shift
- Source: Draft.ts
![Image20191216113622](https://user-images.githubusercontent.com/12394551/70895951-814ed880-1ff8-11ea-9898-00a0508462b4.png)
## 2.1. Trigger
- html:
  - source: views/Document/Draft/Draft.html
- element_stack:
#####
    <div class="draft-page-container">,
    <section v-else class="bcm width100">,
    <v-container class="main-container-draft">,
    <v-layout column align-center justify-center>",
    <v-layout column fill-height d-flex class="bbg width100">,
    <v-layout class="mb-2 pa-2\" justify-space-around align-end>",
    <div @click="voteOnNewSections()">,
    <p class="mf\">{{ inTheVoteSize }} הצעות</p>
## 2.1. Highlighted
    private voteOnNewSections(): void
    
    setNavBar(this.currentRoute.fullPath)
    
    getPath() return `/document/${documentId}/${name}`
    
    push(`/document/springfield/section?sectionsByStatus=0`)
    
    setShowInfoVideo()
## 2.2. Store
## 2.2.1. Display Module
- Source: store/modules/displayModule.ts
##### Highlighted
    navBar
    scrollingOptions
## 2.2.2. Router Module
- Source: store/modules/routerModule.ts
##### Highlighted
    getPath()
    const documentId = rootGetters['mainModule/prettyLink'];
## 2.3.3. Main Module
- Source: store/modules/mainModule.ts
##### Highlighted
    preetyLink
