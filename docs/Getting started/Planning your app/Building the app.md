---
title: Building the app
slug: VGfE-building-the-app
description: Learn how to build an app using JigxBuilder with this comprehensive step-by-step guide. From data setup to testing, discover the process of creating a stunning app with visual enhancements. Explore helpful tips and considerations, including the use of tem
createdAt: Wed Jul 12 2023 18:38:31 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon Jul 17 2023 14:55:35 GMT+0000 (Coordinated Universal Time)
---

Now you are ready to start using your well-designed plan to build the app in Jigx Builder.&#x20;

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/Bke0yOXOJqLaBLdf597x7_buildplan.png" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/Bke0yOXOJqLaBLdf597x7_buildplan.png" size="70" width="436" height="717" position="center" caption="Build plan" alt="Build plan"}

### Steps

1. Start with the data. If you have a pre-existing datasource, create the functions, and stored procedures. If your data source is from scratch, start building the tables using [Dynamic Data](<./../../Building Apps with Jigx/Data/Data Providers/Dynamic Data/Creating tables.md>) or in [Microsoft Azure SQL](<./../../Building Apps with Jigx/Data/Data Providers/Microsoft Azure SQL.md>). Refer to your data plan for details.
2. Next, build out the skeleton app based on must-have functionality, follow your solution design for each screen, and create the corresponding jig file. Choose components and UI elements that meet the requirements. See [examples]() for a list of components, actions, widgets and jigs that can be used.&#x20;
3. &#x20;Now add visual improvements and nice-to-haves. e.g., on an email field, add the email icon to interact with sending an email.&#x20;
4. Publish your app to the Jigx Cloud. Open the app on the mobile device and test each screen, data, and usability. Use [Jigx Dev Tools](<./../../Building Apps with Jigx/Jigx Builder _code editor_/Debugging.md>) to debug the app, make changes and test again.&#x20;
5. When the building of the app is complete, move on to the test plan.
   ![App skeleton](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/BhGW5VVdrGYL6lcJAX4dF_appskeleton.png "App skeleton")

### Considerations

- If you not sure what component, action or widget to use in your app build - get inspired by using [Templates](<./../../Building Apps with Jigx/UI/Jigs _screens_/Jig Templates.md>), the Jigx-sample, and the Jigx-widget projects in <a href="https://github.com/jigx-com/jigx-samples/tree/main/quickstart" target="_blank">GitHub</a>.
- When selecting the elements to add to the YAML, consider the usability, and shortest steps possible to get to where you want in the app.&#x20;
- Minimize navigation, aim for smart navigation, 30 -40 second engagement on screens, especially forms.
- Have the required input fields on the form with optional fields in another section.
- Jigx design methodology encourages 30-second success. This is important as mobile development is different from Web, and space is limited.

### Tips

- Create a prototype using [Templates](<./../../Building Apps with Jigx/UI/Jigs _screens_/Jig Templates.md>) to see if a component or jig will work in your build, from there, you can customize the template YAML snippet.
- Practice continous testing by testing after building each screen.


