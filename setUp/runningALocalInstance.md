# Running a Local Development Instance

## Stroll Portal - Front End

Assuming you have setup your development environment the following steps should not be too hard.

1. Open your terminal if not already open.
2. Run `cd [path to wherever you put what you are working on]`.
3. Run `npm run git:dev` this will checkout to the Demo branch, pull it to the most current version and install the necessary packages, you will need to enter the password for the repo though.
4. Run `npm run startJavaJar`, this will start the local gateway server and allow you to access the backend.
5. Run `npm run start` or `npm start` to start the provider node server, if working on the patient portal you will need to run `npm run start:patient`, this will set the appropriate flags necessary for local development of the patient portal.
6. Run `npm run webpack` for the provider version or `npm run webpack:patient` for the patient version - this will start the webpack service with the appropriate flags in places, in particular it will watch files for changes and rewebpack as needed automatically.
7. Navigate to `localhost:9080` on your browser.
8. As tests develop `npm run test:dev` will start the testing software and run all the tests for the file you are working on as you change the file.
9. Code

**Manual Way**
1. Run `cd [path to wherever you put what you are working on]`.
2. Run `git checkout origin Demo`, this is the main branch you will be working from.
3. Run `npm install` or `npm i`, this will install all the required dependencies in `package.json`.
4. Run `java -jar api-gateway-0.0.1-SNAPSHOT.jar com.sh.mictroservices.gateway.ApiGatewayApp`, this will start the local gateway server and allow you to access the backend.
**NOTE:** You will need to be on a secure network in order to connect to the server.
5. Run `npm start`, this needs to be done in a separate terminal tab/window. Running this command will start a the node server serving the frontend content.  On the react app this will also run a webpack build process before it starts the server.
6. Navigate to `localhost:9080` on your browser.
7. Open a new terminal tab or window and run `webpack --watch` this will keep your bundle.js and styles.css current as you change them.
7. Open another new terminal tab or window and run `npm run test:dev` this will start the testing software and run all the tests for the file you are working as you change the file, ie. when you save, and display the full output of the test.
8. Code
