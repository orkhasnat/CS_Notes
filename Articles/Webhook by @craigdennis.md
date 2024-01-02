# Understanding Webhooks

## Unit 1  - Integration

In this unit we will focus on combining applications together. We'll do this by handling events triggered by applications.

### Video 1 - Welcome

#### Prerequisites

- 🍿 [APIs for Beginners - freeCodeCamp](https://www.youtube.com/watch?v=WXsD0ZgxjRw-us&feature=youtu.be)

#### Learn more

- 📚 [freeCodeCamp.org](https://freecodecamp.org)
- 🍿[freeCodeCamp on YouTube](https://www.youtube.com/freecodecamp) provides a wonderful collection of beginning programming courses. I recommend the [🎥 JavaScript](https://www.youtube.com/watch?v=PkZNo7MFNFg) tutorial.

### Video 2 - Defining Events, Handlers, and Hooks

- 📚 [Web Events](https://developer.mozilla.org/en-US/docs/Web/Events)

#### Learn more

- 📚 [Event Driven Programming](https://wiki.c2.com/?EventDrivenProgramming)

### Video 3 - Lightbulb moment

#### Ideas

- 💡 Think about the weather. Do you want to use the light if it gets rainy/snowy/chilly/hot?
- 💡 What about your location? Want to trigger something when you leave a certain area at a certain time?
- 💡 Think about notifications you get on your phone. Would those be cool to light up the weird dog lamp thing?
- 💡 What about controlling your lights based on a text message?

#### Learn more

- 🐶 🛋️ The dog lamp [LIFX lightbulb](https://www.lifx.com/collections/lamps-and-pendants/products/lifx-color-a19)

### Video 4 - Finding Inspiration

## Unit 2 - Capturing Data from a Webhook

In this unit we'll take a look at a specific Webhook implementations [GitHub](https://github.com) and [Discord](https://discord.com).

### Video 1 - Diving into Webhooks

- 📰 [First blog post about "Web hooks" - Wayback machine](https://web.archive.org/web/20180630220036/http://progrium.com/blog/2007/05/03/web-hooks-to-revolutionize-the-web/)
- 📹 [Web Hooks and the Programmable World of Tomorrow- 2009 talk about Webhooks @ Google](https://www.youtube.com/watch?v=Fw8EPrIjCOc)

### Video 2 - Explore the Request

- 🧰 [Beeceptor](https://beeceptor.com)

#### Learn more

- 🎮 [TwilioQuest - The Flame of Open Source - Learn to use GitHub](https://www.twilio.com/quest/learn/open-source?utm_source=freecodecamp&utm_medium=github&utm_campaign=webhooks)

### Video 3 - Using the Data

- [Best Developer Communities to be a part of in 2020 - freeCodeCamp.org](https://www.freecodecamp.org/news/best-developer-communities-to-be-part-of-in-2020/)

### Video 4 - Developing Locally

⚠️ I made a mistake! I cloned in my `~/Code` directory because I forgot to `cd courses`.

#### Installations

- 🍿 [What is the terminal and why should I use it? - Developer Fundamentals - YouTube](https://youtu.be/lZ7Kix9bjPI)
- 🍿 [What is the file system and why should I learn about it? - Developer Fundamentals - YouTube](https://youtu.be/2zLQwOiIac8)
- [14 ways to open Command Prompt in Windows 10](https://www.digitalcitizen.life/open-cmd/)
- [Install Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [Install Node](https://nodejs.org/en/download/)
- [Install npm](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm)
- [Install Visual Studio Code](https://code.visualstudio.com/download)
- [Optional - Connect GitHub with ssh](https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/connecting-to-github-with-ssh)

### Video 5 - Opening a Tunnel

#### Installations

- 🍿 [What is my System Path? - Developer Fundamentals - YouTube](https://youtu.be/43zdpmEu4lE?utm_campaign=youtube-dev-acq-to--int&utm_source=youtube&utm_medium=dev&utm_content=fcc-api&utm_term=twiliodevs)
- [Install ngrok](https://ngrok.com)
- [Install ngrok to your path - Stack Overflow](https://stackoverflow.com/questions/30188582/ngrok-command-not-found)

Install [nodemon](https://www.npmjs.com/package/nodemon):

```bash
npm install -g nodemon
```

#### Learn more

- 🍿 [The making of ngrok - Alan Shreve (ngrok)](https://www.youtube.com/watch?v=F_xNOVY96Ng)

### Video 6 - Serverless

* [Netlify](https://www.netlify.com)

```bash
npm install netlify-cli -g
```

#### Learn more

- [Making asynchronous programming easier with async and await
](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Async_await)
- [Netlify Dev - Local server](https://www.netlify.com/products/dev/)
- [Cloud Computing Providers - GitHub](https://github.com/tmrts/awesome-cloud-computing)
- 🍿 [What do tutorials mean when they say my shell? - Developer Fundamentals - YouTube](https://youtu.be/fhv2dX0axeY?utm_campaign=youtube-dev-acq-to--int&utm_source=youtube&utm_medium=dev&utm_content=fcc-api&utm_term=twiliodevs)

#### 🖊 Correction

📓 I figured out what my problem was! After you change environment variables in Netlify, you need to re-deploy. That's the reason it worked once I re-deployed it. I decided to keep the bugs in there so you know that **we all make mistakes**. Also it should give you some first hand knowledge of how to debug a webhook.

I hope you enjoy the lemonade made from the lemons of that bit 🍋s.

### Unit 3 - Hooking it altogether

In this unit we'll build an entire application that leans almost entirely on the concept of Webhooks. We'll build an idea capturing hotline that transcribes the ideas and then sends you a text message.

### Video 1 - Introducing the projects

### Video 2 - Text Affirmation

- [Twilio Signup](https://www.twilio.com?utm_campaign=youtube-dev-acq-to--int&utm_source=youtube&utm_medium=dev&utm_content=fcc-api&utm_term=twiliodevs)
- [How to use your free trial account - Twilio Docs](https://www.twilio.com/docs/usage/tutorials/how-to-use-your-free-trial-account)

The following [TwiML](https://twilio.com/docs/sms/twiml) will send a text message when set up to handle incoming messages.

```xml
<Response>
    <Message>You got this!💪</Message>
</Response>
```

This is using a Webhook. When the message comes in, control is passed to your application (it just happens to be in a TwiML Bin), and you return these instructions.

#### 📚 Learn more

- 📚 [`<Message>` - Twilio Docs](https://www.twilio.com/docs/sms/twiml/message)
- 📚 [TwiML Bins](https://www.twilio.com/docs/runtime/tutorials/twiml-bins)

### Video 3 - Setting up the flow

#### Learn more

- 📚 [`<Say>` - Twilio docs](https://www.twilio.com/docs/voice/twiml/say)
- 📚 [Polly Neural voices - Amazon docs](https://docs.aws.amazon.com/polly/latest/dg/NTTS-main.html)
- 🧰 [Twilio Studio](https://twilio.com/studio)

### Video 4 - Handle things locally

- 📚 [Twilio CLI Quickstart](https://www.twilio.com/docs/twilio-cli/quickstart)

```bash
npm install twilio-cli -g
```

Optionally on a Mac, you could use [Homebrew](https://brew.sh)

```bash
brew tap twilio/brew && brew install twilio
```

Install the [Serverless Toolkit](https://www.twilio.com/docs/labs/serverless-toolkit) plugin:

```bash
twilio plugins:install @twilio-labs/plugin-serverless
```

Serverless Function boilerplate:

```javascript
exports.handler = (context, event, callback) => {
  callback(null, "Hi mom!");
};
```

Start your local development server

```bash
twilio serverless:start
```

### Video 5 - Deploying your serverless function

```bash
twilio serverless:deploy
```

### Video 6 - That’s a Wrap

* 🎮 [TwilioQuest - Learn to code and save the cloud](https://www.twilio.com/quest?utm_source=freecodecamp&utm_medium=github&utm_campaign=webhooks)
