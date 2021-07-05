- [Set Up](#set-up)
- [Introduction](#introduction)

[![Netlify Status](https://api.netlify.com/api/v1/badges/2aa5b74a-73cd-42c0-9586-aaf789f8c25f/deploy-status)](https://app.netlify.com/sites/consenz-master/deploys)
# 1. <a id="set-up">Set Up</a>
## 1.1. Install
npm install
## 1.2. Start server
npm run serve
- Starts Server on firebase mode - Get the model data from Firebase
- .env.firebase should have firebase application configuration
## 1.3. Start server in mockdata mode
npm run serve:mockdata
- Starts Server on firebase mode - Get the model data from Firebase
- .env.mockdata should have mockdata configuration.
## 1.4. Test functionality
Make sure it executes [known working features](https://github.com/wonderfloyd/Consenz_Requierments/blob/master/working_features.md/#top)

# 2. <a id="introduction">Introduction</a>
## 2.1. Project Overview
- [Project Overview](./documentation/README.md#top)
## 2.2. <a id="live-demo">Live Demo</a>
[app.consenz.co.il](https://app.consenz.co.il)
- The production demo is connected to Firebase and Firestore for authentication and DB usage.
- The production code uses javascript vuex-easy-firestore and other firebase libs to sync vuex store models with Firestore

