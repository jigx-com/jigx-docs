# Combine the solution's elements

In the [Build your first Jigx solution](https://docs.jigx.com/create-an-app-from-scratch) steps, you have already built a map using the [jig.default](https://docs.jigx.com/examples/jigdefault), added a calendar using the [jig.calendar](https://docs.jigx.com/examples/jigcalendar), added a new customer form using the [jig.default](https://docs.jigx.com/examples/jigdefault), and a customer list using [jig.list](https://docs.jigx.com/examples/jiglist).

Now you can expand the solution further by using the [jig.composite](https://docs.jigx.com/examples/jigcomposite) type to group the new customer jig and the customer list jig into one jig, and add a jig header to the new customer jig.

:::hint{type="success"}
We recommend you build out all the solution steps for the [Create an app from scratch](), as each solution step builds on the previous step until you have a functioning mobile app.
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

You can download the :Link[Hello Jigx solution]{href="https://github.com/jigx-com/jigx-samples/tree/main/quickstart/hello-jigx-solution" newTab="true" hasDisabledNofollow="false"} project on GitHub or build it yourself by following the detailed steps in this section.
