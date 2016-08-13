# Running a Local Development Instance

## Stroll Portal - Front End

Assuming you have setup your development environment the following steps should not be too hard.

1. Open your terminal if not already open.
2. Run `cd [path to wherever you put what you are working on]`.
If working on the front end
3. Run `npm install`, this will install all the required dependencies in `package.json`.
4. Run `java -jar api-gateway-0.0.1-SNAPSHOT.jar com.sh.mictroservices.gateway.ApiGatewayApp`, this will start the gateway development and allow you to access the backend.
5. Run `npm start`, this needs to be done in a separate terminal tab/window. Running this command will start a the node server serving the frontend content.  On the react app this will also run a webpack build process before it starts the server.
6. Navigate to `localhost:9080` on your browser.
7. Open a new terminal tab or window and run `webpack --watch` this will keep your bundle.js and styles.css current as you change them.
7. Open another new terminal tab or window and run `npm run test:dev` this will start the testing software and run all the tests for the file you are working as you change the file, ie. when you save, and display the full output of the test.
8. Code!
9. You'll probably want to run ` find . -name "*.hot-update.*" -type f -delete` from time to time to clear you hot-updates dur
