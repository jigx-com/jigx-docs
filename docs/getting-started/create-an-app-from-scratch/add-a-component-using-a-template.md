---
title: Add a component using a template
slug: j5xL-add-a
createdAt: Fri May 26 2023 08:17:21 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Nov 01 2023 07:06:39 GMT+0000 (Coordinated Universal Time)
description: >-
  Learn how to easily add a signature component template to your project using
  the default Jig template. This step-by-step guide provides detailed
  instructions with helpful screenshots on how to incorpo
---

# Add a component using a template

We have used the default jig template to add a profile jig to the project in the previous step. Let's go ahead and add a component template. Component templates allow you to quickly build up your solution by inserting the required component into the jig file.

In our solution, we have a new customer form, when we signup the new customer we want them to sign the form. Let's use the signature component template to do this.

::Image\[]{alt="Signature component template" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/YHS5JHLDbaSEOC2wxoVab\_customersign.PNG" size="30" caption="Signature component template" position="center"}

1. In Explorer in the **jigs** folder, right-click on the **new-customer.jigx** file.
2. Components are normally added under a `children` node in the YAML. Under the last `component.email-field` section just above the `actions` node place your cursor in the correct node position in the YAML editor and press the **ctrl+space** keys. The Jigx component IntelliSense popup displays listing the available components.

![Component template](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/XWnhFE68Dms4AtWbvYEaB_templatesign.png)

3\. Scroll to the bottom and select **Use template**. The template gallery opens providing the templates for various components. Use the _Search_ and _category_ fields to find the signature template or browse the gallery by scrolling through the options.

![Template gallery](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/XQR2OY2wYrJeYWlM6_Jip_templateselect.png)

4\. Hover over the**Form signature field** template and click the blue **insert** button.

![Insert template](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/25VZeS6vbUmIyU1InExjW_templateinsert.png)

5\. The template YAML will be inserted into your jig file.

![Inserted YAML](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/56Mnfm1qw3DQ83nuTWkPb_templatecode.png)

6\. Publish your project and tap on the new customer widget on the Home Hub in the app. See the signature component on the form.
