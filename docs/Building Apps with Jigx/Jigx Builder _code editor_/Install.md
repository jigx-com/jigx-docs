---
title: Install
slug: YTuR3fevGBdf445PfjTKG
description: Learn how to install and manage the JigxBuilder extension in Visual Studio Code with this comprehensive guide. Discover the steps for installation, updating, and uninstallation, along with valuable insights on utilizing Git integration for effective Jigx 
createdAt: Thu Jul 28 2022 09:09:06 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Feb 14 2024 11:28:48 GMT+0000 (Coordinated Universal Time)
---

This section covers installing the Jigx Builder extension, versions, updates, uninstalling, and the recommended source control. The numbered image below indicates each of these areas in the Jigx Builder.

![Jigx Builder installed](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/F0M0aR2ftgSINpjbqd9yV_jb-extension.png "Jigx Builder installed")

## 1. Install steps

1. Start by downloading and installing VS Code on your development machine. The download is available from [https://code.visualstudio.com/download](https://code.visualstudio.com/download).
2. The Jigx Builder extension is in the <a href="https://marketplace.visualstudio.com/items?itemName=Jigx.jigx-builder" target="_blank">Microsoft Visual Studio Marketplace</a>. Click on the VS Code extension icon in the left navigation bar and search for Jigx Builder.
3. Click the blue **install** button.
4. The Jigx Builder now appears under your list of installed extensions, and is automatically added to the side bar, and is identifiable by its unique icon.

## 2. Versions

The current version of the Jigx Builder extension is shown at the top of the *Extension: Jigx Builder* screen. When a new version is available VS Code automatically installs the latest version and prompts you to reload VS Code.

## 3. Updates

When a new version is available VS Code automatically installs the latest version and prompts you to reload VS Code. Refer to the changelog tab in the *Extension: Jigx Builder* screen to see what changes are included in the new version. If you prefer to manually update the extension see VS Code documentation - <a href="https://code.visualstudio.com/docs/editor/extension-marketplace#_manage-extensions" target="_blank">Manage extensions.</a>

## 4. Uninstall steps

1. To uninstall the Jigx Builder, click on the extensions icon in VS Code.
2. Click the blue **Uninstall** button in the *Extension: Jigx Builder* screen.
3. You can also uninstall the extension by clicking on the **Manage** gear icon at the top right of the extension and selecting **Uninstall.**
4. Reload VS Code.

## 5. Source Control

Manage your Jigx solutions with Git integration in VS Code. See <a href="https://code.visualstudio.com/docs/sourcecontrol/overview" target="_blank">using Git source control in VS Code</a> for more information. When a solution in Jigx Builder is connected to a Git repository the files in the side bar will show in green when a new file is added, yellow for files that have been modified, redwhen there are validation issues that need to be addressed, or *white* when files are commited.

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
In Jigx Management under [Solution Settings](<./../../Administration/Solutions/Solution Settings.md>) you can store the details of your Jigx solution's sourcecode repository, allowing people to easily find the details and contribute to the solution.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/BqDiVPonlfhAP6DK4fhVP_m-sourcecodedetails.png" size="76" position="center" caption="Sourcecode details" alt="Sourcecode details"}


:::
::::



