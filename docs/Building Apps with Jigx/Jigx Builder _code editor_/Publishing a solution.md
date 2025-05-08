---
title: Publishing a solution
slug: aJP2-publishing-a-solution
description: Learn how to publish solutions in JigxBuilder to Jigx Cloud with this step-by-step document. Discover the option to publish the full solution or a single file, and understand how published solutions are automatically added to the Solutions section in Jigx
createdAt: Tue Jun 20 2023 08:34:29 GMT+0000 (Coordinated Universal Time)
updatedAt: Tue Apr 29 2025 11:45:24 GMT+0000 (Coordinated Universal Time)
---

After building the solution in Jigx Builder, you publish the solution to Jigx Cloud. The solution is immediately available in the Jigx App.

You can publish the full solution or choose to publish a single file. Publishing the full solution is required on the first publish. Single file publishing is useful if you made a change to only one file and want to publish the changes or you working on a solution with multiple developers and you only want to publish your changes. Note that the index.jigx file is a shared file that people all work on, so the last updates on the server get published.

## Permissions

When a solution is published, the solution is automatically added to [Solutions](./../../Administration/Solutions.md) in Jigx Management.  The creator of the solution is given Owner permissions and can give users access to the solution in Jigx Management, define their role in the solution scope, and assign `Solution Group` membership for the visibility of widgets.

## Publishing steps

### Full solution

To publish the **entire** solution, follow the steps below:

1. In VS Code click on the Jigx Builder **icon** in the left navigation bar.
2. In the Jigx Explorer hover over the solution node till you see the **publish icon (rocket)**.
   ![Publish icon ](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/x6oL1j00INlbD0HMcaF2U_jb-publish.png "Publish icon")
3. Click on the icon to start the publishing process.
4. Enter your Jigx username and press **Enter**.
5. Enter your Jigx password and press **Enter**.
6. The publishing process starts and the progress shows in the bottom right corner of the VS Code editor. A message displays when the solution is successfully published.

### Single files

To publish a **single** file in the solution follow the steps below:

1. In Jigx Builder locate the file in the side bar explorer that you want to publish.
2. Right-click on the file and click **Publish Jigx file**. Alternatively you can use the shortcut keys given below.
   ![File Publish](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/jZGBiTENpyn7lPsJstAJT_jb-singlepub.png "File publish")

## Publishing shortcuts

| **Shortcuts**                      | **Mac** | **Windows** |
| ---------------------------------- | ------- | ----------- |
| Publish all files in Jigx solution | ⌘R⌘R    | Alt+R Alt+R |
| Publish an individual file         | ⌘R⌘F    | Alt+R Alt+F |

## Viewing published solutions in the app

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
With* *Jigx you can build and publish more than one solution to your Jigx mobile app,  you can switch between the solutions by tapping on the *More* ellipsis icon in the navigation bar and *selecting* the solution you want to use. The currently active solution is highlighted with a checkmark icon.
:::

:::VerticalSplitItem
![Solution switching](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-_wNc-4qfpMvnhWhjpKEx8-20250429-113930.png "Solution switching")
:::
::::



