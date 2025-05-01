---
title: Add the solution stories jig and datasource
slug: J_Kb-add-the-solution-stories-jig-and-datasource
description: Learn how to create a dedicated area on HomeHub for showcasing news, videos, announcements, URLs, and images with this easy-to-follow document. Includes step-by-step instructions, sample code, and tips to create a story jig with an image component that li
createdAt: Tue Apr 11 2023 17:24:37 GMT+0000 (Coordinated Universal Time)
updatedAt: Tue Jun 18 2024 11:47:52 GMT+0000 (Coordinated Universal Time)
---

# Overview

In this step, you will learn how to create a dedicated area on the Home Hub for content, such as news, announcements, videos, URLs, or images. The area is added using [stories](). You will create the story file using the `component.story-group` and a static datasource to reference two images with a title.&#x20;

## Steps

### Create a datasource file for the story jig

1. You need to add the data that the solution story jig can read from. For this step, you create a `Static Datasource` in the datasource folder of the project. The data specifies the description, title, and image for the story. **Right-click** on the datasources node in Explorer and select **New file**.
2. Name the file **story-static. **The file opens and shows the Jigx's auto-complete popup listing the datasource types. Click on **Static datasource** to open the skeleton YAML created by the Jigx Builder.&#x20;
3. You will add an `image`, `titles`, `thumbnails`, and `descriptions` as the data for displaying the story jig. &#x20;
4. See the sample datasource code below for adding the image details for the story jig to display. Save the project.

:::CodeblockTabs
story-static.jigx

```yaml
# A global static datasource that allows easy access and reusability to the data across various jigs and components
type: datasource.static
options:
  data:
    # Description of the datasource. This is not a required field and can be omitted
    - description: My customers
    # The type of data followed by the datasource, in this case an image URL
      image: https://images.unsplash.com/photo-1456324504439-367cee3b3c32?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1740&q=80
      thumbnail: https://images.unsplash.com/photo-1513128034602-7814ccaddd4e?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=870&q=80
      # Name for thumbnail that is displayed on the image
      title: Work productivity
```
:::

### Create a story to a jig

1. Open the Hello- Jigx solution in the Jigx Builder in VS Code, right-click on the jigs node in Explorer, and select New file.
2. Name the file **solution-story**. The file opens and shows the Jigx's auto-complete popup listing the five jig types. Click on **Default** to open the skeleton YAML created by the Jigx Builder
3. &#x20;Give the jig a title called *My customer story* and provide a description like *Customer story*.&#x20;
4. For this jig you can delete the `header` ,  `onFocus`, and `datasource` lines.
5. For the container to display the story add an `entity component` with an `entity field` as shown in the code below:

:::CodeblockTabs
YAML

```yaml
children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Story
            value: Customer
```
:::

6\. Now you can add the story that will be displayed in the dedicated area at the top of the Home Hub. Under the children node type `stories:`, the auto selection pops up, select stories to open the skeleton YAML . Under data add an expression to reference the data from the story-static.jigx datasource file. Add `data: =@ctx.datasources.story-static`. You can add a `groupName:` that displays on the story. You can add your own or use *My work day.*

7\. Under `Item:` you need to define the item type, in this solution, add the `component: image` type as the datasource is an image. Add the title field by adding the following expression to reference the title from the datasource file `title: =@ctx.current.item.title`. Add a `subtitle: =@ctx.current.item.description`. Add the source of the image by using an expression  `source:`  `uri: =@ctx.current.item.image`. Lastly, add the following to open a web site when the story is pressed.
`onPress:`&#x20;
&#x20;        `  type: action.open-url
          options:
            title: Read More
            url: https://docs.jigx.com/stories  `

8\. Your stories node should resemble the code below. Save the project.

:::CodeblockTabs
YAML

```yaml
stories:
 type: component.story-group
  options:
    data: =@ctx.datasources.story-static
    groupName: My work day
    item:
      type: component.image
      options:
        title: =@ctx.current.item.title
        subtitle: =@ctx.current.item.description
        source:
          uri: =@ctx.datasources.story-static.image
        onPress: 
          type: action.open-url
          options:
            title: Read More
            url: https://docs.jigx.com/stories
```
:::

9\. Your solution-story.jigx file should resemble the code below.&#x20;

:::CodeblockTabs
solution-story.jigx

```yaml
# The system name that uniquely identifies the jig
title: My customer story
# The jig type used to display data
type: jig.default

# The controls that will be displayed on the jig are defined under the children node on a default jig 
children:
  - type: component.entity
    options:
      children:
      #Entity fields display data from a datasource
        - type: component.entity-field
          options:
            label: Story
            value: Customer
# Stories are a dedicated area on the home hub screen used to display content such as images, videos, news and announcements 
stories:
# Stories can be grouped together to create a carousel effect that users can swipe through
  type: component.story-group  
  options:
    data: =@ctx.datasources.story-static
    groupName: My work day
    item:
     # This component is used to display an image    
      type: component.image
      options:
        title: =@ctx.current.item.title
        subtitle: =@ctx.current.item.description
        source:
          uri: =@ctx.datasources.story-static.image
        onPress: 
          type: action.open-url
          options:
            title: Read More
            url: https://docs.jigx.com/stories
```
:::

