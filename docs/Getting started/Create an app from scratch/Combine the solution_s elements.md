---
title: Combine the solution's elements
slug: 3KiK-hello-jigx-solution
description: Learn how to expand the Jigx solution by grouping the new customer form and customer list using jig.composite type. Add a Jig header to the new customer Jig and style the solution by adding Stories above the widgets in the HomeHub. Follow the step-by-step
createdAt: Tue Apr 11 2023 11:38:07 GMT+0000 (Coordinated Universal Time)
updatedAt: Fri Feb 21 2025 14:21:29 GMT+0000 (Coordinated Universal Time)
---

In the [Build your first Jigx solution]() steps, you have already built a map using the [jig.default](), added a calendar using the [jig.calendar](), added a new customer form using the [jig.default](), and a customer list using [jig.list]().

Now you can expand the solution further by using the [jig.composite]() type to group the new customer  jig and the customer list jig into one jig, and add a jig header to the new customer jig.

:::hint{type="success"}
We recommend you build out all the solution steps for the [Create an app from scratch](docId:8SeLgEopqiL70vPoV72WY), as each solution step builds on the previous step until you have a functioning mobile app.
:::

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
## Steps

1. Open the Hello-Jigx - Solution in Jigx Builder in VS Code.
2. [Add the customer composite jig](<./Combine the solution_s elements/Add the customer composite jig.md>) file that joins the new customer form and list into one jig using the new-customer and list-customer `jigIds` and add a `header` for the jig.
3. [Edit the index.jigx file](<./Combine the solution_s elements/Edit the index_jigx file.md>), add the customer composite jigId, remove the new customer and the list customer jigIds.
4. [Publish your project](<./Create the Calendar/Publish your project.md>).
5. [Run the updated solution](<./Create the Calendar/Run the updated solution.md>) in the Jigx mobile app, click on each jig to view the solution, note on the customer jig the form, and list display in the same jig.
:::

:::VerticalSplitItem
![Hello Jigx solution](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/U6UJjBwLz27s_ddvuFwZo_hellojigxsolution.PNG "Hello Jigx solution")
:::
::::

## GitHub Samples

You can download the <a href="https://github.com/jigx-com/jigx-samples/tree/main/quickstart/hello-jigx-solution" target="_blank"> Hello Jigx solution project</a>on GitHub or build it yourself by following the detailed steps in this section.

