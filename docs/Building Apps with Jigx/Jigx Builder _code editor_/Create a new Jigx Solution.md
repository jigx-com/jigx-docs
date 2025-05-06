---
title: Create a new Jigx Solution
slug: 01r5-creating-a-new-solution
description: Learn how to create a Jigx app using JigxBuilder and publish it to Jigx Cloud. Follow the step-by-step guide to build a unique title, system name, category, and location for your app. Start by opening VSCode, creating a new Jigx solution, and editing the 
createdAt: Tue Jun 20 2023 08:34:30 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Feb 12 2025 18:39:01 GMT+0000 (Coordinated Universal Time)
---

Creating a Jigx App starts with building a solution in Jigx Builder, then [publishing](<./Publishing a solution.md>) the solution to Jigx Cloud.

## Solution requirements

Every Jigx solution requires the following:

- **Solution title** -  the solution title is visible at the top of the [home hub](<./../UI/Home Hub.md>) screen in the app. Ensure that the title is unique, as there is no validation on the name, which could result in overwriting an existing solution with the same title.
- **Solution name** - The solution name is the system name and Jigx derives the name from the solution title with the following rules applied:
  - Cannot start with a number
  - No spaces are allowed; hyphens replace spaces
  - It must be in lowercase
- **Solution category** - Provides a list of predefined categories to choose from. The category you select displays as a tag at the top of your solution in the [Home Hub](<./../UI/Home Hub.md>) under the solution title in the app.
- **Solution location** - either on your local machine or in a Git repository.
- **Index.jigx** - The index.jigx file is the home screen for the app. Add tabs to determine the layout. See [Home Hub](<./../UI/Home Hub.md>) and [Index settings](<./../UI/Home Hub/Index settings.md>) for more information. 

::embed[]{url="https://vimeo.com/829859076?share=copy"}

## Steps

1. Open VS Code, and click on the Jigx Builder **icon** in the left navigation bar. Select the **Create New Jigx Solution** button.
2. Provide a **solution title **and press enter.&#x20;
3. The **Solution name** field pre-populates with the solution's system name. You can provide a different solution name if you want.
4. Select a relevant **category** where you want the solution saved.
5. Select a local folder or Git repository where the project files are saved too.
6. Your Jigx [solution scaffolding](./Editor.md) opens in the VS Code editor with the .jigx extensions ready for editing.

Follow the steps in the getting started section to [build your first Jigx solution]().
