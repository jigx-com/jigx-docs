# Editor

To accelerate the build experience, Jigx Builder has a YAML editor that includes IntelliSense for code completion, predefined code snippets, and preloads with scaffolding ready to add your Jigx files in the correct structure needed to build app solutions.

## Solution scaffolding

By default Jigx creates scaffolding when loading a new project in Jigx Builder. We recommend avoiding naming new files with the same name in the scaffolding. Words used by the Jigx system include actions, components, jig, databases, datasources, functions, and index.

| Folder              | Default File         | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| ------------------- | -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| .vscode             | settings.json        | Relates to your Jigx solution and contains internal parameter settings required by Jigx Builder runtime. This file's scope is local (workspace) and applies to the current solution. For more information, see <a href="https://code.visualstudio.com/docs/getstarted/settings" target="_blank">https\://code.visualstudio.com/docs/getstarted/settings</a>[https://code.visualstudio.com/docs/getstarted/settings](https://code.visualstudio.com/docs/getstarted/settings) VS code settings. |
| actions             |                      | Actions refer to specific controls or operations responding to an event or input. Create [global actions](./../UI/Actions.md) under the actions folder to define actions once and reuse them multiple times in different jigs.                                                                                                                                                                                                                                                                |
| assets              |                      | The solution's images and icons defined under the [Assets](./../UI/Assets.md) folder will preload and cache when the solution downloads or updates in the app.  Allows images and icons to display when the app is offline and improves the app's performance.                                                                                                                                                                                                                                |
| databases           | default.jigx         | You can use the `default.jigx` file to define the tables in the [Dynamic Data](<./../Data/Data Providers/Dynamic Data.md>) Provider.                                                                                                                                                                                                                                                                                                                                                          |
| datasources         |                      | Create global data files with .jigx extension- these are available for use in your whole solution to any of the jigs.                                                                                                                                                                                                                                                                                                                                                                         |
| functions           | myfirstfunction.jigx | You can build logic into your solution by adding functions to get or update data from a remote service, such as [REST Functions](<./../../Administration/Solutions/REST Functions.md>) or [SQL Functions](<./../../Administration/Solutions/SQL Functions.md>).                                                                                                                                                                                                                               |
| jigs                | myfirstjig.jigx      | The jigs folder is where you create all the files used to configure the screens for the app on your mobile device. You can create sub-folders inside the jigs folder for categorization. All files in the jigs folder must have the `.jigx` extension, e.g.,  leave-form.jigx                                                                                                                                                                                                                 |
| translations        |                      | Create files for various languages using localization, then reference the file in your jig using the `Text Locale` property with `id: file name`. For more information, see [Localization](<./../Additional functionality/Localization.md>).                                                                                                                                                                                                                                                  |
|                     | index.jigx           | The index.jigx file is the app's home screen. It uses bottom tabs to determine the layout. See [Home Hub](<./../UI/Home Hub.md>) and [Index settings](<./../UI/Home Hub/Index settings.md>) for more information.                                                                                                                                                                                                                                                                             |
| scripts/expressions |                      | Create .js files to define your [JavaScript functions](#) that can be used in [expressions](./../Logic/Expressions.md).                                                                                                                                                                                                                                                                                                                                                                       |

## IntelliSense

To invoke IntelliSense, simultaneously press the control and spacebar (ctrl+space) keys. The code popup displays only valid options in the current cursor context. Selecting an option from the IntelliSense menu will load the code snippet with the necessary properties for that option.

::embed[]{url="https://vimeo.com/829865905?share=copy"}

## YAML indentation

In Jigx Builder the YAML code snippets use indentation. The nested structure of the YAML is visible with spaces, not tabs, and is used for indentation. Each nested level is indented further than its parent, illustrating the hierarchical structure of the YAML file. Line numbers are visible on the left side, and your cursor blinks at one of the lines. You can use a VS Code plugin to highlight the indention levels in different colors. One such plugin is **Indent-Rainbow **<a href="https://marketplace.visualstudio.com/items?itemName=oderwat.indent-rainbow" target="_blank">https\://marketplace.visualstudio.com/items?itemName=oderwat.indent-rainbow</a>[https://marketplace.visualstudio.com/items?itemName=oderwat.indent-rainbow](https://marketplace.visualstudio.com/items?itemName=oderwat.indent-rainbow) [https://marketplace.visualstudio.com/items?itemName=oderwat.indent-rainbow](https://marketplace.visualstudio.com/items?itemName=oderwat.indent-rainbow).&#x20;

![Indentation levels in color](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/QymqO8OqTZoINMMdQJ4MM_jb-colorindent.png "Indentation levels in color")

## Code snippets

Code snippets are there to help you develop quicker by providing you with recommended  properties to use for a jig type, component, action, or widget. You do not need to use all the code snippets provided; you can remove the unwanted properties.

![IntelliSense & code snippets](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/kr7nZdObHWrTB_Fo7vYDJ_jb-intellisensecode.gif "IntelliSense & code snippets")

## Validation

Jigx validates the structure and values in the `.jigx` YAML files and shows the issues that you need to fix.

![Validation ](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/SX0T3-ddqxxV15RWT7Lpg_jb-validation.png "Validation ")

Validation issues are shown in:

- The **file name** in the side bar will be red, with the number of issues in the file shown by a red number on the right of the file name.
- **Red squiggles** appear under the YAML. Hover over the YAML for more information, if we can detect what the value should be we offer a quick-fix link. Clicking on the link will fix the issue and resolve the validation.
- In the **Problems tab** of the Jigx Dev tools window, the file and a description of the issue is shown. Click on the item to go to the exact ssue in the file.

:::hint{type="warning"}
Validation does not always prevent you from publishing your solution. The solution on the mobile app might not function as expected if the validation issues are not resolved.
:::

## Validation - Solution diagnostics

**Jigx Solution Diagnostics **is a built-in analysis tool that helps you identify and troubleshoot issues across your entire Jigx solution or a subset of files in the solution. It detects project build errors, missing references, and scans your source code for programmatic errors, warnings, and overall solution health.

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
### Running Solutions Diagnostics

You can access the Jigx Solution Diagnostics tool through the **Jigx Explorer **by clicking the diagnostics icon, or by pressing **fn+F1 **and selecting Run Jigx Solution Diagnostics**.**

To run the tool on a subset of files, press fn+F1** **and select **Run Jigx Solution Diagnostics – with filter**. Then, provide a regular expression (regex) to filter and analyze only the matching files.

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-XuAgpuvvxhACMGd383TAQ-20250523-115757.png" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-XuAgpuvvxhACMGd383TAQ-20250523-115757.png" size="80" width="956" height="372" position="center" caption="Diagnostics icon" alt="Diagnostics icon"}

![Diagnostics commands](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-eTSwCdtvKI34jrciC8c4i-20250523-115854.png "Diagnostics commands")
:::

:::VerticalSplitItem
### Solutions Diagnostics progress

The progress is shown as a **notification** in the bottom-right of the VS code window.&#x20;

![](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-au-5XQOC20nuylo-jJoYu-20250523-120010.png)


:::
::::

When the diagnostics run is complete, the results are displayed in the **Jigx Output **panel. The output includes the file path, a description of the issue, and the number of issues found in each file. You can navigate to the relevant file to review and resolve the errors.

:::hint{type="warning"}
The URL to open the file in the Jigx ouput panel will not work if the folder contains spaces.
:::

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-5_JLFUdoHEQzdgUY5kImn-20250523-120107.png" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-5_JLFUdoHEQzdgUY5kImn-20250523-120107.png" size="92" width="2396" height="1162" position="center" caption="Jigx output" alt="Jigx output"}

## Navigating code definitions & references

This feature is particularly useful in large projects or when working with unfamiliar codebases, as it helps you understand how and where certain pieces of code are implemented without manually searching through files. If the code has multiple definitions or references, VS Code presents a list of all these instances, allowing you to choose the one you're interested in.

The following code definitions and references can be navigated:

- fileId references
  - jigs
  - linkTo, jigId
  - datasources
  - ctx.datasources.datasourceName
  - functions
  - components
  - actions
- entity references
  - databases/default.jigx
  - entity, entities
- components references
  - instanceId, @ctx.components.componentInstanceId...
- script references
  - JavaScript functions

### Definition (F12)

![](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/Fngvr94bdyeeid19lLKhU_jb-godef.gif)

Place your cursor on the code and press **F12** or right-click and select **Go to Definition** from the menu options, VS Code displays a preview window that lists all the lines of code in your project where that code is used, either in the same jig or another file in the project. VS Code will open the file where that code is defined and move the cursor to the definition's location.

### References (shift+F12)

![](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/cShnfmtfqWELAanH7yGDT_jb-f12-goref.gif)

Place your cursor on the code and press **Shift + F12** or right-click and select **Go to References **from the menu options, VS Code displays a preview window that lists all the lines of code in your project where that code is used or referenced. If there are multiple references, you can click on any of the listed references in the preview window to go directly to that location in the code.
