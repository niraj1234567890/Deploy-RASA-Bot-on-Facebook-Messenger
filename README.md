# Deploy-RASA-Bot-on-Facebook-Messenger

There are so many bots running accross a various platforms. Building a bot on your local computer is one part of a complete bot development process but it is incomplete without deploying it on the major messeging servies like messenger. Lets learn how to deploy RASA based bot on Facebook-Messenger.

### Basic Step
Having a totally working fine bot on your local computer without any error is must before going forward into this domain.
Also you should have all the required files for bot in a single folder as per RASA standard
So make sure you have one, if you don't have one you can use a bot developed by me [**A Funny ChatBot**](my another repo). 
1. You can download the repo in your computer and start using it for deployment process.
          [make sure you have all the required libraries installed in your computer]
2. set your current working directory a folder where you have downloaded above mentioend repo
3. run following commands on individual terminal
          **rasa run actions**
          **rasa run -m models --endpoints endpoints.yml --credentials credentials.yml**
          **ngrok http 5005**
**NOTE:-** edit credentials.yml file after getting credentials in (**First Step**--->>> 3. **getting credentials**) as mentioned in that step
### First Step
For deploying your bot on messenger, you have to do the following work on facebook:
1. **set up a facebook page**
      - Go to facebook.com/pages/create
      - Click to choose a Page type
      - Fill out the required information.
      - Click Continue and follow the on-screen instructions
2. **create a FB app**
      - Go to [Facebook for Developers](https://developers.facebook.com) and click on **My Apps** → **Add New App**.
3. **getting credentials**      
      - Go onto the dashboard for the app and under **Products**, find the **Messenger** section and click **Set Up**. Scroll         down to **Token Generation**
      - Select your page and select it in the dropdown menu for the **Token Generation**. The shown **Page Access Token** is         the ***page-access-token*** needed later on.
      - Locate the **App Secret** in the app dashboard under **Settings** → **Basic**. This will be your ***secret***
      - Use the collected ***secret*** and ***page-access-token*** in your **credentials.yml**, and add a field called               ***verify*** containing a string of your choice

### What is a webhook?
- It is a running server where your bot is working
- The Messenger Platform sends events to your webhook to notify your bot when a person sends a message. Webhook events are     sent by the Messenger Platform as POST requests to your webhook.
### What is an ngrok?
- It generates a public URLs for any localhost URL(two public URLs)
- Now we can make an HTTP request to any generated URLs and it will route to the localhost URL
- A generated public URLs, one of them is **http** and other one is **https**[SSL secured]
    
4. **setting up a webhook**
        **rasa run -m models --endpoints endpoints.yml --credentials credentials.yml**
        This command will run a server in your localhost on port 5005, and this server will work as a webhook for your FB             messenger app
        **NOTE**:- make sure you have added your credentials in credentials.yml file as mentioned above
5. **verifying a webhook**
      - Before messenger sends any HTTP request to your webhook, it will verify your webhook with using a callBack URL and a ***verify**
      - callBack URL must be secured(https) but our bot is running on a localhost and it is http, so we can make use of               **ngrok** to generate a secured public URL, run this following command on terminal after installing ngrok in your             computer
        **ngrok http 5005**
      - copy https version of generated URL and paste it to the below location
      app's main page ->>>>messenger->>>>settings->>>>>webhooks->>>>>callBack URL
      - add **/webhooks/facebook/webhook** in above URL
        Final URL will look like: **https:<ngrok_url>/webhooks/facebook/webhook**
      - and put value of ***verify*** into **Verify Token**
      Enter verify and bammmmmm.
      Your webhook is verified.
