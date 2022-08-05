# Sandbox App for Jared

## Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in your browser.

The page will reload when you make changes.\
You may also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can't go back!**

If you aren't satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you're on your own.

You don't have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn't feel obligated to use this feature. However we understand that this tool wouldn't be useful if you couldn't customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Code Splitting

This section has moved here: [https://facebook.github.io/create-react-app/docs/code-splitting](https://facebook.github.io/create-react-app/docs/code-splitting)

### Analyzing the Bundle Size

This section has moved here: [https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size](https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size)

### Making a Progressive Web App

This section has moved here: [https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app](https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app)

### Advanced Configuration

This section has moved here: [https://facebook.github.io/create-react-app/docs/advanced-configuration](https://facebook.github.io/create-react-app/docs/advanced-configuration)

### Deployment

This section has moved here: [https://facebook.github.io/create-react-app/docs/deployment](https://facebook.github.io/create-react-app/docs/deployment)

### `npm run build` fails to minify

This section has moved here: [https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify](https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify)




# Jared's Notes

Here, we will follow and take notes on making a small, full stack application
using AWS, React, \& GraphQL.

## Module 1: Deploy and Host a React App

### 1.1: Create a new react application.

We use the commands:
```
npx create-react-app amplifyapp
cd amplifyapp
npm start
```
npx is an alias for `npm exec` which essentially runs a command
from a local or remote npm package.

In this case, `create-react-package` is the package we're using.
It then asks you to install it in the runtime.

### 1.2 Initialize a github repository

Create your package in a directory as shown above,
then simply make it a github repository

### 1.3 Log into AWS Management Console

Basically go to the AWS Console, and open the amplify tool

### 1.4 Deploy

There are two options:
1. Develop
2. Deploy
Option #2 allows us to develop locally, and deploy as a github branch!
How easy is that!

Pretty much step through the prompts until the app begins to deploy.
It will then trigger and re-deploy every time you push to a specific branch!

### 1.5 The Code!
I'm seeing mostly JS and css scripts as well as an svg (data)

#### index.js
Which I'm sure aligns with the layout (left panel?)

#### tests

#### App.js
looks like it have the primary logic

## Module 2: Initialize a local amplify app

### install

```
npm install -g @aws-amplify/cli
```

### configure

**???** I'm still pretty confused how the configration of an amplify
project is directly connected to a single user. I guess this is because whereever local code is kept, you may want to limit permissions.
This is why every amplify cli is associate with a single user? Hmm

This section made me set up the accessKeyID etc for User of the account
where I set up my own permissions as Admin? I guess?

### Initialize the app

Get the `appId`

```
(base) ➜  amplifyapp git:(main) ✗ amplify pull --appId d1pzrdl11rgf5x --envName staging
Opening link: https://us-west-2.admin.amplifyapp.com/admin/d1pzrdl11rgf5x/staging/verify/?loginVersion=1
⠋ Confirm login in the browser or manually paste in your CLI login key:
✔ Successfully received Amplify Studio tokens.
Amplify AppID found: d1pzrdl11rgf5x. Amplify App name is: amplifyapp
Backend environment staging found in Amplify Console app: amplifyapp
? Choose your default editor: Vim (via Terminal, macOS only)
? Choose the type of app that you're building javascript
Please tell us about your project
? What javascript framework are you using react
? Source Directory Path:  src
? Distribution Directory Path: build
? Build Command:  npm run-script build
? Start Command: npm run-script start
? Do you plan on modifying this backend? Yes
✔ Successfully pulled backend environment staging from the cloud.
✅

Successfully pulled backend environment staging from the cloud.
Run 'amplify pull' to sync future upstream changes.
```

at anytime you can access either the Amplify, or AWS console using:
```
(base) ➜  amplifyapp git:(main) ✗ amplify console
✔ Which site do you want to open? · AWS console
https://us-west-2.console.aws.amazon.com/amplify/home?region=us-west-2#/d1pzrdl11rgf5x/YmFja2VuZA/staging
```

### Module 3:

#### Add authentication

It seems that amplify comes with some tools for helping setup the
backend.

Yea these are just nice templates for setting up regular backend
infrastructure within the project.

```
amplify add auth
```

#### Deploy

```
amplify push
```

Huh, so now amplify has a push method
for adding local configurations.
My guess is that pushing the anything that's added
let's the amplify service know which types of dependencies you
need in order to

#### Edit the Build script

In the amplify console, on the leftside toolbar,
there are build settings where you find the script to
edit. Add build targets for the new backend.

In this case. our amplify scipt looks like this:

```
version: 1
backend:
  phases:
    build:
      commands:
        - '# Execute Amplify CLI with the helper script'
        - amplifyPush --simple
frontend:
  phases:
    preBuild:
      commands:
        - npm ci
    build:
      commands:
        - npm run build
  artifacts:
    baseDirectory: build
    files:
      - '**/*'
  cache:
```

Note - This could either be at the top of the repository, or
kept within the console.

#### Set up CI/CD

In the main page of the app, you will have to specify the "environment"
that you created. The environment that you create is taken from theconsole when you search for backend. Pulling that with
```
$ amplify pull <X>
```
**???** is what allows you to have your privlages etc?
You defined that environment when you went to the main
app page, and above the preview window clicked on backend. You basically named a backend there. Right

Bingo!
```
Next, we will deploy a back end and initialize the backend environment locally.
```
This was the step where we, yea, did the thing above this quote in M2

Then you can modify even more?
or develop locally with that environment, I'm assuming.

For building, you need to make sure that the container
that is given by default has what you need to build and run / deploy
an app. When I messed up I had to update my amplify CLI on the server side by doing [this](https://repost.aws/questions/QUSCAhS9GuRN2J_5f3tKe1dQ/how-do-you-update-amplify-build-version-for-ci-cd)

For example, when we added authntication, we first pulled in the
environment, added some changes, and pushed the result. Those
changes were the result of modifying the code and node_modules I assume
After you edite those, you proabably need to have the added
dependencies installed locally. When we added auth, I noticed
the `package.json` file then included:

```
  5   "dependencies": {
  6     "@aws-amplify/ui-react": "^3.2.1",          <-- this was new.
  7     "@testing-library/jest-dom": "^5.16.4",
  8     "@testing-library/react": "^13.3.0",
  9     "@testing-library/user-event": "^13.5.0",
 10     "aws-amplify": "^4.3.30",                   <-- This was new.
 11     "react": "^18.2.0",
 12     "react-dom": "^18.2.0",
 13     "react-scripts": "5.0.1",
 14     "web-vitals": "^2.1.4"
 15   },
```

Ah. so then it would be good to try and make a more slimmed down
version of the Dockerfile - you could then build this image locally
and simply keep up to date with that - to make sure local builds
will be the exact same as deployment builds.


### Module 4

#### Amplify API tool

```
(base) ➜  sandboxapp git:(main) ✗ amplify add api
? Select from one of the below mentioned services: GraphQL
? Here is the GraphQL API that we will create. Select a setting to edit or con
tinue Continue
? Choose a schema template: One-to-many relationship (e.g., “Blogs” with “Post
s” and “Comments”)

⚠️  WARNING: your GraphQL API currently allows public create, read, update, and delete access to all models via an API Key. To configure PRODUCTION-READY authorization rules, review: https://docs.amplify.aws/cli/graphql/authorization-rules

✅ GraphQL schema compiled successfully.

Edit your schema at /home/jared/agora-dev/sandboxapp/amplify/backend/api/sandboxapp/schema.graphql or place .graphql files in a directory at /home/jared/agora-dev/sandboxapp/amplify/backend/api/sandboxapp/schema
✔ Do you want to edit the schema now? (Y/n) · yes
Couldn’t find selected code editor (sublime) on your machine.
? Try opening with system-default editor instead? No
✅ Successfully added resource sandboxapp locally

✅ Some next steps:
"amplify push" will build all your local backend resources and provision it in the cloud
"amplify publish" will build all your local backend and frontend resources (if you have hosting category added) and provision it in the cloud
```

So we're adding a database API? I don't know why they're not saying
that more explicitly.

I guess thinking a little more about this, really, the front
end is designed specifically to request things from the backend.
So when a user clicks on something, it sends a request to the backend
(in this case using a graphql schema). So the backend API is pretty
much just a set of queries based upon user requests from the
frontend.

#### Designing the API 'schema's'

The first thing we're asked to do after adding qraphql
api via amplify, is to edit `amplfy/backend/api/myapi/schema.graphql`
It starts with:

```
(base) *[main][~/agora-dev/sandboxapp/amplify/backend/api/sandboxapp]$ cat schema.graphql


# This "input" configures a global authorization rule to enable public access to
# all models in this schema. Learn more about authorization rules here: https://docs.amplify.aws/cli/graphql/authorization-rules
input AMPLIFY { globalAuthRule: AuthRule = { allow: public } } # FOR TESTING ONLY!

type Blog @model {
  id: ID!
  name: String!
  posts: [Post] @hasMany
}

type Post @model {
  id: ID!
  title: String!
  blog: Blog @belongsTo
  comments: [Comment] @hasMany
}

type Comment @model {
  id: ID!
  post: Post @belongsTo
  content: String!
}
```

From the link above:
>> Use the @auth directive to configure authorization rules for public, sign-in user, per user, and per user group data access. Authorization rules operate on the deny-by-default principle. Meaning that if an authorization rule is not specifically configured, it is denied.

?? What does it mean "all models in this schema". I guess the
schema defines data models which are pretty much defining the
data a specific model contains, who can access it, 
as well as it's relationship to other models (data base tables?).

Moving on, the tutorial now want to update the schema with

```
type Note @model {
  id: ID!
  name: String!
  description: String
}
```

**???** I wonder what tf a `!` means behind a datatype ...

#### Deploy the API

Okay, so now we will deploy the API to the cloud
```
amplify push --y
```
This does 3 things:
1. Create the AppSync API
2. Create a DynamoDB table
3. Create the local GraphQL operations in a folder located at src/graphql that you can use to query the API

Output:
```
(base) *[main][~/agora-dev/sandboxapp/amplify/backend/api/sandboxapp]$ amplify
push --y
⠹ Fetching updates to backend environment: staging from the cloud.⠋ Building re
⠹ Fetching updates to backend environment: staging from the cloud.
⚠️  WARNING: your GraphQL API currently allows public create, read, update, and delete access to all models via an API Key. To configure PRODUCTION-READY authorization rules, review: https://docs.amplify.aws/cli/graphql/authorization-rules

✅ GraphQL schema compiled successfully.

Edit your schema at /home/jared/agora-dev/sandboxapp/amplify/backend/api/sandboxapp/schema.graphql or place .graphql files in a directory at /home/jared/agora-dev/sandboxapp/amplify/backend/api/sandboxapp/schema
✔ Successfully pulled backend environment staging from the cloud.
⠦ Building resource api/sandboxapp
⚠️  WARNING: your GraphQL API currently allows public create, read, update, and delete access to all models via an API Key. To configure PRODUCTION-READY authorization rules, review: https://docs.amplify.aws/cli/graphql/authorization-rules

✅ GraphQL schema compiled successfully.

Edit your schema at /home/jared/agora-dev/sandboxapp/amplify/backend/api/sandboxapp/schema.graphql or place .graphql files in a directory at /home/jared/agora-dev/sandboxapp/amplify/backend/api/sandboxapp/schema

    Current Environment: staging

┌──────────┬────────────────────┬───────────┬───────────────────┐
│ Category │ Resource name      │ Operation │ Provider plugin   │
├──────────┼────────────────────┼───────────┼───────────────────┤
│ Api      │ sandboxapp         │ Create    │ awscloudformation │
├──────────┼────────────────────┼───────────┼───────────────────┤
│ Auth     │ sandboxappc8037494 │ No Change │ awscloudformation │
└──────────┴────────────────────┴───────────┴───────────────────┘

⚠️  WARNING: your GraphQL API currently allows public create, read, update, and delete access to all models via an API Key. To configure PRODUCTION-READY authorization rules, review: https://docs.amplify.aws/cli/graphql/authorization-rules

✅ GraphQL schema compiled successfully.

Edit your schema at /home/jared/agora-dev/sandboxapp/amplify/backend/api/sandboxapp/schema.graphql or place .graphql files in a directory at /home/jared/agora-dev/sandboxapp/amplify/backend/api/sandboxapp/schema
⠇ Building resource api/sandboxapp
⚠️  WARNING: your GraphQL API currently allows public create, read, update, and delete access to all models via an API Key. To configure PRODUCTION-READY authorization rules, review: https://docs.amplify.aws/cli/graphql/authorization-rules

✅ GraphQL schema compiled successfully.

Edit your schema at /home/jared/agora-dev/sandboxapp/amplify/backend/api/sandboxapp/schema.graphql or place .graphql files in a directory at /home/jared/agora-dev/sandboxapp/amplify/backend/api/sandboxapp/schema
⠹ Updating resources in the cloud. This may take a few minutes...

UPDATE_IN_PROGRESS amplify-amplifyf6d807b6f50e4-staging-70045 AWS::CloudFormation::Stack Thu Aug 04 2022 18:18:39 GMT-0600 (Mountain Daylight Time) User Initiated
CREATE_IN_PROGRESS apisandboxapp                              AWS::CloudFormation::Stack Thu Aug 04 2022 18:18:44 GMT-0600 (Mountain Daylight Time)           
.
.
.

CREATE_COMPLETE                     apisandboxapp                              AWS::CloudFormation::Stack Thu Aug 04 2022 18:22:17 GMT-0600 (Mountain Daylight Time)
UPDATE_COMPLETE_CLEANUP_IN_PROGRESS amplify-amplifyf6d807b6f50e4-staging-70045 AWS::CloudFormation::Stack Thu Aug 04 2022 18:22:20 GMT-0600 (Mountain Daylight Time)
UPDATE_COMPLETE                     authsandboxappc8037494                     AWS::CloudFormation::Stack Thu Aug 04 2022 18:22:22 GMT-0600 (Mountain Daylight Time)
UPDATE_COMPLETE                     amplify-amplifyf6d807b6f50e4-staging-70045 AWS::CloudFormation::Stack Thu Aug 04 2022 18:22:22 GMT-0600 (Mountain Daylight Time)
✔ Generated GraphQL operations successfully and saved at ../../../../src/graphql
⠋ Uploading files...⠋ Uploading files...⠋ Uploading files...⠋ Uploading files...⠋ Uploading files...⠋ Uploading files...⠋ Uploading files...⠋ Uploading files.
✔ All resources are updated in the cloud

GraphQL endpoint: https://l7x3le5lp5c5lbf5gaq4djwf2i.appsync-api.us-west-2.amazonaws.com/graphql
GraphQL API KEY: da2-7mialqfmlzcf7kvhj6nv4g2aae

GraphQL transformer version: 2
```

OK so after this is done we just added a bunch more code to `App.js`

Primarily, the App function now has three primary nested functions:

> There are 3 main functions in our app:

1. fetchNotes - This function uses the API class to send a query to the GraphQL API and retrieve a list of notes.
2. createNote - This function also uses the API class to send a mutation to the 
GraphQL API, the main difference is that in this function we are passing in the variables needed for a GraphQL mutation so that we can create a new note with the form data.
3. deleteNote - Like createNote, this function is sending a GraphQL mutation 
along with some variables, but instead of creating a note we are deleting a note.

* a little shitshow. While this is nice I'm starting to think the obfuscation of AWS amplify is a little too much to learn.

Either way, I just fought a bug. Turned out I just needed to feed
a fucking parameter into the main App function called signOut, 
even though I never imported such a thing. Like, how tf does this work?

```
<Button onClick={signOut}>Sign Out</Button>
```
I guess react just gives you special tags for adding elements to a web
page. These tags have arguments like a function you want to call.
I still want to know where `signOut` comes from.


### Add storage

This is where we're going to connect the backend to S3 buckets.

```
(base) λ agorahackbox sandboxapp → λ git main* → amplify add storage
? Select from one of the below mentioned services: Content (Images, audio, video, etc.)
✔ Provide a friendly name for your resource that will be used to label this category in the project: · imagestorage
✔ Provide bucket name: · sandbox-image-storage-bucket
✔ Who should have access: · Auth users only
✔ What kind of access do you want for Authenticated users? · create/update, read, delete
✔ Do you want to add a Lambda Trigger for your S3 Bucket? (y/N) · no
✅ Successfully added resource imagestorage locally

⚠️ If a user is part of a user pool group, run "amplify update storage" to enable IAM group policies for CRUD operations
✅ Some next steps:
"amplify push" builds all of your local backend resources and provisions them in the cloud
"amplify publish" builds all of your local backend and front-end resources (if you added hosting category) and provisions them in the cloud
```

OK, now it wants us to add/update the schema to add images as
an attribute of the Note type.

```
type Note @model {
  id: ID!
  name: String!
  description: String
  image: String
}
```

### amplify push

```
amplify push --y
```

Set up the new infrastructure. 

### More implimentation in `App.js`

Okay, let's break down some of these functions, time for some real
coding baby.

```
+  91   ¦ ¦ <div style={{marginBottom: 30}}>
+  92   ¦ ¦ ¦ {
+  93   ¦ ¦ ¦ ¦ notes.map(note => (
+  94   ¦ ¦ ¦ ¦ ¦ <div key={note.id || note.name}>
+  95   ¦ ¦ ¦ ¦ ¦ ¦ <h2>{note.name}</h2>
+  96   ¦ ¦ ¦ ¦ ¦ ¦ <p>{note.description}</p>
+  97   ¦ ¦ ¦ ¦ ¦ ¦ <button onClick={() => deleteNote(note)}>Delete note</button>
+  98   ¦ ¦ ¦ ¦ ¦ </div>
+  99   ¦ ¦ ¦ ¦ ))
+ 100   ¦ ¦ ¦ }
+ 101   ¦ ¦ </div>
+ 102   ¦ ¦ 
```

to

```
+  91   ¦ ¦ <div style={{marginBottom: 30}}>
+  92   ¦ ¦ ¦ {
+  93   ¦ ¦ ¦ notes.map(note => (
+  94   ¦ ¦ ¦ ¦ ¦<div key={note.id || note.name}>
+  95   ¦ ¦ ¦ ¦ ¦ ¦<h2>{note.name}</h2>
+  96   ¦ ¦ ¦ ¦ ¦ ¦<p>{note.description}</p>
+  97   ¦ ¦ ¦ ¦ ¦ ¦<button onClick={() => deleteNote(note)}>Delete note</button>
+  98   ¦ ¦ ¦ ¦ ¦ ¦{
+  99   ¦ ¦ ¦ ¦ ¦ ¦ ¦note.image && <img src={note.image} style={{width: 400}} />
+ 100   ¦ ¦ ¦ ¦ ¦ ¦}
+ 101   ¦ ¦ ¦ ¦ ¦</div>
+ 102   ¦ ¦ ¦ ¦))
+ 103   ¦ ¦ ¦ }
+ 104   ¦ ¦ </div
```






