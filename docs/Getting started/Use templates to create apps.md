---
title: Use templates to create apps
slug: vBJW-Ha5s0EJ6Ht4s93-e
description: Learn how to create a travel app using a provided template in Jigx Builder. Customize your app by editing the template or adding files. Publish and access it on mobile devices with Jigx app. Explore other app development options with Jigx, including plann
createdAt: Tue Apr 04 2023 06:20:14 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Feb 12 2025 17:54:39 GMT+0000 (Coordinated Universal Time)
---

## What you will create

Create a travel app using one of the provided templates. The template inserts the required YAML in the correct format.  Use the template as a base on which to build when creating a jig. If the template by default provides the functionality you need, publish your Jigx project to use the jig on your mobile device.
**Build time:** 5 mins

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/nhnka5qOCrS2S63wcj5BN_gs-traveltemplate.PNG" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/nhnka5qOCrS2S63wcj5BN_gs-traveltemplate.PNG" size="80" width="2540" height="2500" position="center" caption}

:::hint{type="info"}
Before you start building your first solution, ensure you have created a [Jigx's account](<./Creating an account.md>) and [Install the Jigx Builder](<./Install the Jigx Builder.md>). &#x20;
:::

### Step 1: Create a new solution in Jigx Builder

1. Open VS Code, and click on the Jigx Builder **icon** in the left navigation bar. Select the **Create New Jigx Solution** button.
2. Type **World Travel** in the Solution title field and press enter. This name displays at the top of your solution on the Home Hub in the Jigx App.&#x20;
3. The *Solution name* field automatically pre-populates with the solution's system name world-travel. Press **Enter.**
4. For this solution select the **business** category.&#x20;
5. Select a local folder where the project files are saved too. Your Jigx default solution files open in the VS Code editor with the .jigx extensions ready for editing.

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/AawckxW3PviULalVud-bw_travel-newproject.png" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/AawckxW3PviULalVud-bw_travel-newproject.png" size="86" width="1842" height="1392" position="center" caption="Jigx project in VS code " alt="Jigx project in VS code "}
:::

:::VerticalSplitItem
![Jigx scaffolding](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/kuNAv26MpCnH8iF1IJAPJ_travel-scaffolding.png "Jigx scaffolding")
:::
::::

### Step 2: Choose a template

![Template Configure jig](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/yD3-Ltvoz-MPpTWaSml9v_t-configure.gif "Template Configure jig")

1. In Explorer expand the **jigs** folder and click on `myfirstjig.jigx` file. The Jigx auto-complete popup displays. &#x20;
2. Click on **use template** to open the list of templates.&#x20;
3. Under **Default** hover-over **Default jig 6 **and click the blue insert button.&#x20;
4. The jigx file is populated with the YAML for the template.&#x20;
5. Change the title to ***Thailand*** as the `title` for your jig.&#x20;
6. The `myfirstjig.jigx` file is already referenced in the `index.jigx` file which is the home screen file (Home Hub).

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
![Template option](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/TSiTR6hE6bPW1-TFYpW6j_travel-template.png "Template option")
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/NE_f0eCNadYf8xNTxDdF__travelselect.png" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/NE_f0eCNadYf8xNTxDdF__travelselect.png" size="84" width="2312" height="1686" position="center" caption="Select template" alt="Select template"}
:::
::::

### Step 3: Publish the solution

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
1. In VS Code click on the Jigx Builder** icon** in the left navigation bar.
2. In the Jigx Explorer hover over the **world-travel** node till you see the **publish** **icon (rocket)**. Click on the icon to start the publishing process.&#x20;
3. Enter your Jigx username and press **Enter**.
4. Enter your Jigx password and press **Enter**. The publishing process starts and the progress shows in the bottom right corner of the VS Code editor. A message displays when the solution is successfully published.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/5BYTgK92WvGfXaPO0LCwr_travel-publish.png" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/5BYTgK92WvGfXaPO0LCwr_travel-publish.png" size="84" width="584" height="620" position="center" caption="Publish Jigx project" alt="Publish Jigx project"}
:::
::::

### Step 4: Open the app on your mobile device

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
1. On your mobile device** tap** the Jigx app icon.&#x20;
2. Sign into the app with your [Jigx account](<./Creating an account.md>) details**.**
3. The app opens the [Home Hub](<./../Building Apps with Jigx/UI/Home Hub.md>) screen displaying the **World Travel** solution.
4. Tap on the icon to display the **Thailand** destination screen.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/FTNVTmq5D0UtXCcniFa_i_gs-traveltemplate.PNG" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/FTNVTmq5D0UtXCcniFa_i_gs-traveltemplate.PNG" size="84" width="2540" height="2500" position="center" caption="Jigx template" alt="Jigx template"}
:::
::::

:::hint{type="success"}
Yes it is that simple to build apps in Jigx. Explore further by either editing the YAML in `myfirstjig.jigx`; or adding additional files under the jig folder, add another template, reference the file in `index.jigx` and publish the solution.
:::

## What's next?

Why not build your own app? See how to [plan your app](<./Planning your app.md>), then learn how to [create an app from scratch](<./Create an app from scratch.md>) or explore the various available UI elements in Jigx by adding the **Jigx-samples** [prebuilt solution](<./Use pre-built solutions.md>) to your organization and viewing the solution in the Jigx App.
