# Introduction to APIs

## Unit 1 - What is an API

In this unit we'll define what an API, or Application Programming Interface, is and why you should use them.

### Video 1 - Welcome

👋 Hello and welcome to the course and your notes! Make sure you check this area out often!

#### Beginner content

- [freeCodeCamp.org](https://www.freecodecamp.org/) is a great place to get started and I recommend jumping [right in](https://www.freecodecamp.org/learn/responsive-web-design/basic-html-and-html5/say-hello-to-html-elements).
- 🍿[freeCodeCamp on YouTube](https://www.youtube.com/freecodecamp) provides a wonderful collection of beginning programming courses. I recommend the [🎥 JavaScript](https://www.youtube.com/watch?v=PkZNo7MFNFg) tutorial.

#### Designing API Content

- 📚 [REST API Design Best Practices - freeCodeCamp](https://www.freecodecamp.org/news/rest-api-design-best-practices-build-a-rest-api/)
- 🍿 [What exactly is an API - ProgrammableWeb 101](https://www.youtube.com/watch?v=cpRcK4GS068&list=PLcgRuP1JhcBP8Kh0MC53GH_pxqfOhTVLa)
- 📚 [API Guide - moesif](https://www.moesif.com/blog/api-guide/)

### Video 2 - Defining Interface

#### Learn more

##### Media Player APIs

Don't worry about understanding these, however, appreciate their complexity

- [Android MediaPlayer API documentation](https://developer.android.com/reference/android/media/MediaPlayer)
- [iOS Media Player API documentation](https://developer.apple.com/documentation/mediaplayer)
- [Web Audio API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API)

### Video 3 - Defining API

#### Learn more

- 📚 [Web APIs - MDN](https://developer.mozilla.org/en-US/docs/Web/API)
- 📰 [Google vs. Oracle on the rights to the Java API - The Verge](https://www.theverge.com/2019/11/15/20946398/oracle-google-java-copyright-lawsuit-trial-supreme-court-request)
- 

### Video 4 - Remote APIs

#### The path to remote APIs

- [SOAP - Wikipedia](https://en.wikipedia.org/wiki/SOAP)
- [Remote Procedure Call (RPC) - Wikipedia](https://en.wikipedia.org/wiki/Remote_procedure_call)
- [SOAP and REST at Odds](https://thehistoryoftheweb.com/soap-rest-odds/)
- [SOAP vs. REST](https://stackify.com/soap-vs-rest/)
- [REST vs. RPC](https://cloud.google.com/blog/products/application-development/rest-vs-rpc-what-problems-are-you-trying-to-solve-with-your-apis)

### Video 5 - How the web works

- [HTTP - Wikipedia](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol)
- 📚 [How the Web Works - MDN](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/How_the_Web_works)

### Video 6 - RESTful API Constraint Scavenger Hunt

- [Representational State Transfer - Wikipedia](https://en.wikipedia.org/wiki/Representational_state_transfer)

## Unit 2 - Exploring APIs

In this unit, we'll do some hands-on exploring of a couple of popular APIs.

### Video 1 - Exploring an API online

- [Spotify for Developers](https://developer.spotify.com/)
- 🔎[Spotify Console](https://developer.spotify.com/console/)
- 🦞[Beyonce's Spotify Page](https://open.spotify.com/artist/6vWDO969PvNqNYHIOW5v0m)
- Beyonce's Spotify ID: `6vWDO969PvNqNYHIOW5v0m`

#### Explore

- ProgrammableWeb provides [a categorized directory of APIs](https://www.programmableweb.com/category-api). 
- API List provides [categories and a powerful search feature](https://apilist.fun/).

### Video 2 - Using an API from the command line

- 🍿 [What is the terminal and why should I use it? - Developer Fundamentals - YouTube](https://youtu.be/lZ7Kix9bjPI)

#### Installing cURL

##### Mac OS

###### Using Homebrew

```bash
brew install curl
```

###### Download

⬇️ [Download cURL for MacOSX](https://curl.haxx.se/dlwiz/?type=bin&os=Mac+OS+X)

##### Windows

⬇️ [Download cURL for Windows](https://curl.haxx.se/windows/)

**NOTE**: If you are running PowerShell, delete the `curl` alias for `Invoke-WebRequest` by adding the following command to your profile (`C:\Users\<username>\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1)`:

```bash
Remove-Item alias:curl
```

#### Learn More

- 📚 [Command Line for Beginners – How to Use the Terminal Like a Pro - freeCodeCamp](https://www.freecodecamp.org/news/command-line-for-beginners/)
- Check out the [jq tutorial](https://stedolan.github.io/jq/tutorial/) for parsing JSON on the command line
- [cURL manpage](https://curl.haxx.se/docs/manpage.html)
- [POST (HTTP) - Wikipedia](https://en.wikipedia.org/wiki/POST_(HTTP)) (For info on `form-urlencoded` search for "Use for submitting web forms")

### Video 3 - You Go Curl

- 🙌 [Twilio - Signup](https://www.twilio.com/try-twilio?utm_campaign=youtube-dev-acq-to--int&utm_source=youtube&utm_medium=dev&utm_content=fcc-api&utm_term=twiliodevs)
- [Twilio Console](https://twilio.com/console?utm_source=gh-link&utm_medium=referral&utm_campaign=intro-to-apis)
- 📚 [Create a Message - Twilio Docs](https://www.twilio.com/docs/sms/api/message-resource?code-sample=code-create-a-message&code-language=curl&code-sdk-version=json&utm_campaign=youtube-dev-acq-to--int&utm_source=youtube&utm_medium=dev&utm_content=fcc-api&utm_term=twiliodevs)

The Twilio `Messages` API URL is:

```bash
https://api.twilio.com/2010-04-01/Accounts/<Your Account SID Here>/Messages.json
```

Make sure to replace that `SID` with your Account SID which can be found in the [Twilio console](https://twilio.com/console)

### Video 4 - Using Tools to Explore APIs

- 💡 [Govee Aura Smart Table Lamp](https://us.govee.com/products/aura-table-lamp)
- ⬇️ [RestFox (REST API Client)](https://restfox.dev)

### Video 5 - More tools for your API Exploring Toolbox
- ⬇️ [Visual Studio Code (code editor)](https://code.visualstudio.com)
- ⬇️ [Thunder Client for VS Code](https://www.thunderclient.com/)
- 🎓🆓 [Postman Student Expert Certification Program](https://bit.ly/postman-student-expert-fcc)
- 🍿 [Postman Webinars](https://www.postman.com/webinars/)
- ⬇️ Many wonderful API Collections can be downloaded for exploration in the [Postman API Network](https://postman.com/explore)

#### Learn More

- [Boilerplate code - Wikipedia](https://en.wikipedia.org/wiki/Boilerplate_code)

### Video 6 - Using Helper Libraries 

- 🍿 [What is the file system and why should I learn about it? - Developer Fundamentals - YouTube](https://youtu.be/2zLQwOiIac8)
- [Command Line Interface - VSCode](https://code.visualstudio.com/docs/editor/command-line)
- ⬇️ [Install Node.js (JavaScript runtime)](https://nodejs.org/en/download/)
- 📚 [Promise - mdn](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
- 📚 [Async / Await - mdn](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Async_await)
- 🍿 [What is my System Path? - Developer Fundamentals - YouTube](https://youtu.be/43zdpmEu4lE?utm_campaign=youtube-dev-acq-to--int&utm_source=youtube&utm_medium=dev&utm_content=fcc-api&utm_term=twiliodevs)

To use the [Twilio Node Helper Library](https://www.twilio.com/docs/libraries/node?utm_campaign=youtube-dev-acq-to--int&utm_source=youtube&utm_medium=dev&utm_content=fcc-api&utm_term=twiliodevs#installation)

```bash
npm install twilio
```

**Windows**
Make a directory named `scratch`

```bash
mkdir scratch
```

## Unit 3 - Using APIs

In this unit, we'll build a single page application that makes use of a client side framework and it's APIs. We'll create a server side API to feed our application, and reshape data from a public Web API. That's a lot of APIs!

### Video 1 - Introducing the project

> [!example]- 👩‍💻 The code
> ```html
> <!DOCTYPE html>
> <html lang="en">
>   <head>
>     <meta charset="UTF-8" />
>     <meta http-equiv="X-UA-Compatible" content="IE=edge" />
>     <meta name="viewport" content="width=device-width, initial-scale=1.0" />
>     <link
>       rel="stylesheet"
>       href="https://fonts.googleapis.com/css?family=Open+Sans"
>     />
>     <style>
>       body {
>         font-family: "Open Sans", sans-serif;
>         margin: 5%;
>       }
>     </style>
>     <script src="https://cdn.jsdelivr.net/npm/vue@2.7.13"></script>
>     <script src="https://unpkg.com/vue-silentbox@2.3.1/dist/vue-silentbox.min.js"></script>
>     <title>Pick.le: Pick your pics 🥒</title>
>   </head>
>   <body>
>     <div id="app">
>       <h1>Pick.le: Pick your pics 🥒</h1>
>       <h2>{{ callToAction }}</h2>
>       <silent-box :gallery="gallery"></silent-box>
>     </div>
> 
>     <script>
>       Vue.use(VueSilentbox.default);
>       const app = new Vue({
>         el: "#app",
>         data() {
>           return {
>             callToAction: "Submit your photos of kittehs!",
>             gallery: [],
>           };
>         },
>         methods: {
>           async loadImages() {
>             // TODO: Use the Messaging API to use submitted photos
>             // const response = await fetch("/api/")
>             // TODO: Create a web-based API that matches this expected response
>             this.gallery = [
>               {
>                 src: "https://placekitten.com/200/300",
>                 description: "Look at this kitteh",
>                 alt: "A kitteh",
>                 thumbnailWidth: "200px",
>               },
>               {
>                 src: "https://placekitten.com/300/300",
>                 description: "Another Kitteh",
>                 alt: "Cutie",
>                 thumbnailWidth: "200px",
>               },
>             ];
>           },
>         },
>         mounted() {
>           this.loadImages();
>         },
>       });
>     </script>
>   </body>
> </html>
> ```

- 🍿 [What do tutorials mean when they say my shell? - Developer Fundamentals - YouTube](https://youtu.be/fhv2dX0axeY?utm_campaign=youtube-dev-acq-to--int&utm_source=youtube&utm_medium=dev&utm_content=fcc-api&utm_term=twiliodevs)
- [Vue.js - Front-end JavaScript Framework](https://vuejs.org)
- [Vue SilentBox Plugin](https://github.com/silencesys/silentbox)

**Windows**
To open an HTML file in your default browser from the command line:

```bash
start .\index.html
```

### Video 2 - Serverless
> [!example]- 👩‍💻 The code (/incoming-message)
>```js
> // This is your new function. To start, set the name and path on the left.
> 
> exports.handler = function (context, event, callback) {
>   console.log(`Incoming message: ${event.Body}`);
>   // Here's an example of setting up some TWiML to respond to with this function
>   const twiml = new Twilio.twiml.MessagingResponse();
>   twiml.message("Thanks for your submission! 📸");
>   console.log(`TwiML was ${twiml}`);
>   // This callback is what is returned in response to this function being invoked.
>   // It's really important! E.g. you might respond with TWiML here for a voice or SMS response.
>   // Or you might return JSON data to a studio flow. Don't forget it!
>   return callback(null, twiml);
> };
>```

- [Serverless Computing - Wikipedia](https://en.wikipedia.org/wiki/Serverless_computing)
- [Serverless on Twilio](https://www.twilio.com/en-us/serverless?utm_campaign=youtube-dev-acq-to--int&utm_source=youtube&utm_medium=dev&utm_content=fcc-api&utm_term=twiliodevs)
- 🍿 [Understanding Webhooks - freeCodeCamp - YouTube](https://youtu.be/41NOoEz3Tzc)

### Video 3 - Writing a Server Side API

>[!example]- 👩‍💻 The code (/api/pics)
> ```js
> exports.handler = async function (context, event, callback) {
>   const client = context.getTwilioClient();
>   const gallery = [];
>   
>   /* This is the format we need to match. Here for reference
>     [
>       {
>         src: "https://placekitten.com/200/300",
>         description: "Look at this kitteh",
>         alt: "A kitteh",
>         thumbnailWidth: "200px",
>       },
>     ];
>   */
>   const messages = await client.messages.list({ to: context.TWILIO_NUMBER });
>   for (const message of messages) {
>     // You can have multiple medias on each message
>     const pics = await message.media().list();
>     for (const pic of pics) {
>       // Add to the gallery array, use the outer loop's message value to put the same body
>       // for each pic
>       gallery.push({
>         src: "https://api.twilio.com" + pic.uri.replace(".json", ""),
>         description: message.body,
>         alt: message.body,
>         thumbnailWidth: "200px",
>       });
>     }
>   }
>   // Twilio Function will automatically turn gallery into proper JSON and set the 
>   // header to `application\json`
>   return callback(null, gallery);
> };
>```
- 🤷 [Example NSFW Detection API](https://smartclick.ai/api/nsfw-detection/)
- [Everything You Need To Know About API Rate Limiting - Nordic APIs](https://nordicapis.com/everything-you-need-to-know-about-api-rate-limiting/)

### Video 4 - Fetching Results on the Client from our Server

>[!example]- 👩‍💻 The updated code (index.html)
> ```html
> <!DOCTYPE html>
> <html lang="en">
>   <head>
>     <meta charset="UTF-8" />
>     <meta http-equiv="X-UA-Compatible" content="IE=edge" />
>     <meta name="viewport" content="width=device-width, initial-scale=1.0" />
>     <link
>       rel="stylesheet"
>       href="https://fonts.googleapis.com/css?family=Open+Sans"
>     />
>     <style>
>       body {
>         font-family: "Open Sans", sans-serif;
>         margin: 5%;
>       }
>     </style>
>     <script src="https://cdn.jsdelivr.net/npm/vue@2.7.13"></script>
>     <script src="https://unpkg.com/vue-silentbox@2.3.1/dist/vue-silentbox.min.js"></script>
>     <title>Pick.le: Pick your pics 🥒</title>
>   </head>
>   <body>
>     <div id="app">
>       <h1>Pick.le: Pick your pics 🥒</h1>
>       <h2>{{ callToAction }}</h2>
>       <silent-box :gallery="gallery"></silent-box>
>     </div>
> 
>     <script>
>       Vue.use(VueSilentbox.default);
>       const app = new Vue({
>         el: "#app",
>         data() {
>           return {
>             callToAction: "Submit your photos of burritos!",
>             gallery: [],
>           };
>         },
>         methods: {
>           async loadImages() {
>             // Our API is on the same server so we don't need to specify the host
>             // NOTE: fetch is asynchronous and returns a `Promise`, so we'll `await`
>             const response = await fetch("/api/pics");
>             // NOTE: The `json` method on the response object is also asynchronous
>             // Setting the gallery object automatically causes the API to refresh because
>             // we bound it to the plugin as part of the `data` API of Vue.
>             this.gallery = await response.json();
>           },
>         },
>         mounted() {
>           this.loadImages();
>         },
>       });
>     </script>
>   </body>
> </html>
> ```
- 📚 [fetch API - mdn](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
- 🏅 [REST Architectural Constraints - Scavenger Hunt PRIZE!](https://en.wikipedia.org/wiki/Representational_state_transfer#Architectural_constraints)
- 🍿 [Learn Twilio Messaging, Voice, and Serverless (Full Course!)](https://youtu.be/4jUMqutYmyE?utm_campaign=youtube-dev-acq-to--int&utm_source=youtube&utm_medium=dev&utm_content=fcc-api&utm_term=twiliodevs)
- 

### Video 5 - Wrap Up

I built a little Twilio application using [Studio](https://www.twilio.com/docs/studio?utm_campaign=youtube-dev-acq-to--int&utm_source=youtube&utm_medium=dev&utm_content=fcc-api&utm_term=twiliodevs) and some APIs to gather your feedback.

Please text `FEEDBACK` to me at [(432) 527-4274](tel:+14325274274) and let me know what you thought about this course! (You can also call if that's your jam)

👋 Thanks for hanging out! 🙏 Keep me updated on your journey 💪🚀!

[@craigsdennis](https://twitter.com/craigsdennis)

PS. If you want to keep on learning for free, I can't recommend [the video game TwilioQuest 🎮](https://twilio.com/quest?utm_campaign=youtube-dev-acq-to--int&utm_source=youtube&utm_medium=dev&utm_content=fcc-api&utm_term=twiliodevs) enough.