---
description: >-
  Step-by-step guide on how to test an integration that you have developed and are looking to contribute.
---

# How to Test a Destination Integration

This guide will show you how to test the integration you develop and ensure that everything is working before submitting a pull request.

## Installing RudderStack on Your Developer Machine

For testing purposes, everything should be done on your local machine. Therefore, RudderStack must be downloaded and set up properly. Please follow [this guide](https://docs.rudderstack.com/get-started/installing-and-setting-up-rudderstack/developer-machine-setup) to get RudderStack running on your machine.

The guide above will instruct you on how to get your PostgreSQL database, `rudder-server`, and `rudder-transformer` all installed and running on your local machine. You will also need to install the `config-generator`. Instructions on how to do that can be found [here](https://docs.rudderstack.com/get-started/config-generator#setting-up-the-config-generator).

## Testing Your Transformation

When developing a destination integration for RudderStack, the most important component is the transformation that you develop for the particular destination. When you are finished developing the transformation you can test it in two different ways.
1. Test your transformation by running the test file you developed. Before submitting a pull request you should run a test on all destinations to ensure that they are all working as intended. You can do this by running `npm test` from the terminal. However, testing all destinations takes a long time and can be inefficient when you are only concerned about the transformation you are developing. Therefore, you can run `npm test -- <destination_name>` to just test a single destination at a time.
2. Another way to test your transformation is to navigate to `rudder-transformer` in your terminal and run `npm start`. The `rudder-transformer` should then start running in `PORT: 9090`. Then open Postman (or any similar program) and create a `POST` request that is pointed to `http://localhost:9090/v0/destinations/<destination_name>`. In the JSON body insert the payload you would like to test. The payload structure can be found in the `__tests__/data` folder. Press send to send the request through your transformation and inspect the returned response. Ensure that it matches the format the destination requires it to be.

## Testing Your Config Generator

Another component you must develop is the configuration settings for the integration. To test your code for the `config-generator` first navigate to the folder in your terminal and run `npm start`. If the browser doesn't open automatically you can open your browser and search for `localhost:3000`. Then make the necessary connection from a source to your destination and fill out the settings. Finally, once the connection has been made, you can press the `Export` button in the top right hand corner of the screen. This will download a JSON file called `workspaceConfig.json`. Open this file and ensure that the information is correct.

## Testing End to End

To ensure everything is working as intended, you may want to test the whole stack end to end. This would involve filling out the settings using the `config-generator`. Then updating the `rudder-server` with the `workspaceConfig.json` file and running it. Then, running the `rudder-transformer`. And finally, sending a `POST` request via Postman to audit the response. The following steps will explain, in detail, how to implement this test.

1. Follow the instructions above to produce a `workspaceConfig.json` file via the `config-generator`. Make sure that your source is an HTTP API source so that we can use Postman for testing. Feel free to test using other sources, but this guide will use the HTTP API source and Postman.
2. Save the `workspaceConfig.json` file somewhere in the `rudder-server` repository. Preferably in the `config` folder.
3. Follow [these instructions](https://docs.rudderstack.com/get-started/config-generator#developer-machine-setup) to direct the `rudder-server` to use the config settings from the downloaded `workspaceConfig.json` file. The `configJSONPath` should be `./config/workspaceConfig.json` if it was stored in the `config` folder.
4. Start the `rudder-server` by running this command `go run -mod=vendor main.go` from the terminal in the `rudder-server` directory. It should be running on `PORT: 8080`
5. Start the `rudder-transfomer` by running this command `npm start` from the terminal in the `rudder-transformer` directory. It should be running on `PORT: 9090`
6. Go to Postman and create a `POST` request that is pointed to `http://localhost:8080/v1/<event_type>` where `<event_type>` can be any of the event types i.e. identify, track, page, etc.
7. In the "Auth" tab of Postman, create a "Basic Auth" authorization. For the "Username" insert the write key of the HTTP API source you are sending the event to. Leave the "Password" blank.
8. In the JSON body of the request, insert a RudderStack formatted event. For a template and example of an accetable event, look [here](https://docs.rudderstack.com/rudderstack-api-spec/http-api-specification#6-identify), make sure the event structure matches that of the `<event_type>` you are sending the request to (see step #6).
9. Press send and validate that the event was received by the destination correctly.

## Contact Us

If there are any issues with testing your integration please reach out to us in our [**Slack**](https://resources.rudderstack.com/join-rudderstack-slack) channel.

For more information on any of the sections in this guide, feel free to [**contact us**](mailto:%20docs@rudderstack.com) ****or start a conversation on our [**Slack**](https://resources.rudderstack.com/join-rudderstack-slack) channel.

