# conference-terms-conditions

This is an example of how to embed a button to conference in terms and conditions that will be recorded. While you can use a "secure flow" to do this the customer and IVR is not recorded for compliance as its a secure flow. By "Conferencing" in a flow you can play the recorded messages as well as then the agent can hear it as well as the customers response. This is then also part of the recording and transcription of the interaction.

## Step 1

This example uses "Implicit Grant" OAuth2 to your Genesys Cloud ORG environment. The first thing you will need to do is to get a ClientID from your Genesys Cloud ORG with the ability to connect to the API endpoints. This will also need to have a redirect to the Hosting location of the server url for example: "http://localhost:8080/index.html". You will also need add the required "scopes" for the endpoints that you want to use. In this example we are using "conversations".

![](/docs/images/oauth.png?raw=true)

Save this and copy the

    "clientId"

as you will need this later for the authentication.

## Step 2

Now create the [Architect Inbound Call Flow](https://help.mypurecloud.com/articles/add-the-inbound-call-flow/) and put in the prompts that you want to be played.

![](/docs/images/prompts.png?raw=true)

Ensure that the flow has a disconnect block at the end.

![](/docs/images/flow.png?raw=true)

Now make sure that you "Publish" the flow as well as copy the "flowId" out of the URL so you can use this later on. It will look like this:

![](/docs/images/flowId.png?raw=true)

## Step 3

Create the [Agent Script](https://help.mypurecloud.com/articles/create-script/) This can be editing an existing one you already have or creating a new one. The main thing here is it will allow the Agent to simply press the one button to "Conference" in the flow you built in step 2. To add the code to your script you will need to put in a "Web Page" object with the below URL.

This is dependent on where you host the webpage of course as well as your own clientId and flowId.

    http://localhost:8080/index.html?gc_region=mypurecloud.com.au&gc_clientId=YOUR_CLIENT_ID&gc_redirectUrl=http://localhost:8080/index.html&gc_flowId=YOUR_FLOW_ID&gc_conversationId={{Scripter.Interaction ID}}

NOTE: I'm in the apse2 region so i have the "mypurecloud.com.au" this may differ in your region. The conversationId is being gathered by the default scripter variable. Make sure the you update the other variables with your data from above eg:

    YOUR_CLIENT_ID & YOUR_FLOW_ID

![](/docs/images/script.png?raw=true)

Once you host the html file on a web server this would also be moved form localhost:8080 when this is done remember to also add it as a redirect in your OAuth client you setup earlier.

## Testing

Now your done. Make a call in and when you click on the button as an agent you should get the flow conferenced into the interaction. This will then also be visible in the transcript and heard by both agent and customer for compliance.

![](/docs/images/timeline.png?raw=true)

![](/docs/images/transcript.png?raw=true)
