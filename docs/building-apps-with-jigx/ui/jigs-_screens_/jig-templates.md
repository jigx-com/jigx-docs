---
title: Jig Templates
slug: BfrN-templates
createdAt: Thu May 25 2023 06:10:17 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Feb 12 2025 18:55:49 GMT+0000 (Coordinated Universal Time)
description: >-
  Save time and effort with Jigx's template gallery, offering a wide range of
  solutions for customization. Ensure consistency and reduce development time by
  simply selecting and inserting different temp
---

# Jig Templates

Jigx provides a template gallery that you can use as a base when creating solutions. Jigx templates are available when creating jigs, adding components\*\* \*\*and widgets to a jig.

Using templates has many benefits, such as:

1. **Time Efficiency:** Templates provide a pre-designed structure and layout. They can save you time by eliminating the need to start from scratch or design every aspect from the ground up. With templates, you can jumpstart your development process and focus more on customizing the specific functionality you require.
2. **Consistency and Best Practices:** Templates ensure consistency in your project. Using templates helps maintain a uniform structure, coding style, and user experience throughout your application.
3. **Reduced Development Effort:** Templates include pre-built features and components that are commonly required when building Jigx Apps. By leveraging these pre-existing elements, you can reduce the effort needed to implement standard features, allowing you to allocate more time and resources to develop unique and critical features that differentiate your app.

:::hint{type="info"} While templates offer numerous benefits, it's important to remember that they may not always meet your requirements. Customization is still necessary, and templates should be used as a starting point rather than a complete solution. :::

![Jig template](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/X_s4ibsAS55I6mPhDPISi_templatejig.png)

### Using jig templates

::embed\[]{url="https://youtu.be/Sn0YICgtS60"}

:::hint{type="info"} Jig templates either use [Static Data](https://docs.jigx.com/examples/static) or [Dynamic Data](../../data/data-providers/dynamic-data/dynamic-data.md). You can easily customize the template to use other [datasources](../../../administration/solutions/data.md) instead. :::

Each jig type has a set of templates to choose from. Follow the steps below to select a template.

1. In Explorer in the **jigs** folder, right-click and create a new jig file with the .jigx extension. The Jigx IntelliSense popup displays listing the available jig types and the **Use template** option. Use **ctrl+space to open the jig IntelliSense popup.**

![Jig template option](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/GoeoJRsy4pw59kUTSl5Tv_templatesjigcode.png)

1. Click **Use template**. The templates gallery opens providing the templates for all jig types. Use the _Search_ and _Category_ fields to find the template you want or browse the gallery by scrolling through the options.
2. Once you have chosen a template, hover over the template, there are two options:

**1. Insert**

![Template Insert jig](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/G9FpoCJ94Zfim3LcYjnZd_t-insert.gif)

1. Click the blue **Insert** button. The selected template YAML will be inserted into your jig file.
2. Check the YAML code for comments that specify additional steps you must take on the template, such as _#Create new table invoices in databases/default.jigx_. Here you will manually need to add the table to the `default.jigx` file under the database folder.
3. Add your jigId to the `index.jigx` file.
4. Publish your project and view the jig in the app.
5. Now you can customize the jig by changing the static data to dynamic data or adding additional components using the component templates described below.

**2. Configure**

![Template Configure jig](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/yD3-Ltvoz-MPpTWaSml9v_t-configure.gif)

1. Click the blue **Insert** button.
2. The selected template YAML will be inserted into your jig file.
3. Check the YAML code for comments that specify additional steps you must take on the template, such as _#Create new table invoices in databases/default.jigx_. Here, you will manually need to add the table to the `default.jigx` file under the database folder.
4. The`jigId` are **automatically** added to the index.jigx file.
5. Publish your solution and view the widget and jig in the app.
6. Now you can customize the jig by changing the static data to dynamic data or adding additional components using the component templates described below.

### Scenario templates

You can use the scenario templates to create a functioning solution. For example insert the **Content management** scenario template and publish out the solution to the app. The scenario includes four jigs and adds the contacts Dynamic Data table.

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/RCSQgz3TqyiydLH0ibmBS\_t-scenario.png" size="68" position="center" caption="Scenario templates" alt="Scenario templates"}

#### See Also

* [Component Templates](../components-_controls_/component-templates.md)
