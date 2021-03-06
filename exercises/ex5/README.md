# Exercise 5 - Preparation for Mobile App and Deployment

In this exercise we will prepare our project to be used by a mobile AppGyver application and prepare for deployment. For this we will do two things: First, we will create a new service API explicitly for the mobile app and we will remove the security role checks for the sake of this session. Implementing end-to-end security with authentication and authorization would exceed the scope of our session. Then we will add Cross Origin Resource-Sharing (CORS) support for our services allowing AppGyvver to access the service at design time. Finally we will hit the "Deploy" button.



## Excercise 5.1 Adding Another Service
We only have one data model, but we can expose this model with various services tailored for the need of the consuming user interface or system. For the mobile consumption through AppGyver-based app, which we will create in the next excercise we will create a new service.

on the "Home" tab, click on one of the service entities (e.g. HeroService) which takes you to the "Service Editor". Now click on "New Service" button in the toolbar on top.

![](/exercises/ex5/images/Deploy_01.png)

Provide the name "ConsumerService" and click "Create".

You will see an empty canvas.

We want to expose the "Hero" and the "Order" entity. Let's start with the hero:

Click the "+" sign in the upper toolbar and click "Add Projection". Provide the following values, start using the "Type" drowpdon:

![](/exercises/ex5/images/Deploy_02.png)

and confirm with a click on "Create".

Again, click on the "+" sign on top and choose "Add Projection" to add the following values:

![](/exercises/ex5/images/Deploy_03.png)

confirm by clicking "Create".
Your service should look like this now:

![](/exercises/ex5/images/Deploy_04.png)

Close the "Service Editor" to navigate back to the "Home Screen".

## Exercise 5.2 Adding CORS support
We will now adjust the service definition by hand and modify the code. Yes, you heard right. We do so to demonstate a true differentiator of this Low-Code perspective withing App Studio: the ability to fall back to the code level for full flexibility making sure that the tool will never navigate you into a situation where you are stuck.

Let's select View > Explorer to open the file view of your project. Here you can acually see the technology underneath, which consists of a CAP project and two Fiori Elements apps at the moment. 

In order to let AppGyver access our sevices we need to add CORS support to our service. This is pretty straightforward. First, open a Terminal by selecting Terminal > New Terminal from the main menu. The terminal will open as a prompt at the bottom of your screen. Type:
```bash
npm i cors
```
this command will add an external module from the npm repository as a dependeny to your project. (you can check the package.json in your main directoy if you want).

![](/exercises/ex5/images/Deploy_05.png)

Now, in the left-hand menu, expand the "srv" directory and check its content. Now, right-click on the "srv" folder and select "New File" from the context-menu. Name the new file "server.js". A text editor will appear any you can copy the following code into it:

```JAVASCRIPT
"use strict";

const cds = require("@sap/cds");
const cors = require("cors");
cds.on("bootstrap", app => app.use(cors()));

module.exports = cds.server;
```

![](/exercises/ex5/images/Deploy_06.png)

We will now check if our new service is running in preview mode. 
It should look like this:

![](/exercises/ex5/images/Deploy_07.png)

## Exercise 5.3 Deploy to "Production"

Now that we have prepared everything, click "Deploy" on the "Home" screen.
You are then asked to log on. Confirm the Cloud Foundry Endpoint (https://api.cf.eu10.hana.ondemand.com), then provide the email address and the password of you user ( TecEdLCAP001+0XX@gmail.com where xx is the number you got earlier ).
That's it. That's all. Really.

While we are waiting for the deplyoment to happen we will switch tools and start working with AppGyver in the next exercise.

## Summary
This conclued this exercise and we have a complete application deployed, incl. a SAP HANA database, some web apps and some APIs. Not bad.

Continue to - [Preparation](../exPrep/README.md)
