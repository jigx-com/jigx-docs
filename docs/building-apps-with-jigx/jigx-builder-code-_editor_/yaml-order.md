---
title: YAML order
slug: k3-h-yaml
createdAt: Tue Dec 12 2023 12:00:59 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Feb 12 2025 18:42:25 GMT+0000 (Coordinated Universal Time)
---

# YAML order

When it comes to ordering YAML elements, it's crucial to structure your Jigx file in a clear and logical manner. By doing so, you can ensure that your YAML data is easy to read, maintain, and troubleshoot, and sometimes, even the performance and order of execution are determined by the order.

Here are the best practices for ordering YAML elements in a jig file and the recommended structure for items in a section, for example, components.

{% hint style="info" %}
You won't necessarily use every element listed below in a single jig. You can modify the list to suit the elements you are including in your jig.
{% endhint %}

### Jig YAML order

* Title
* Description
* Type
* Icon
* Badge
* Inputs
* Placeholders
* onFocus/onRefresh
* Expressions
* header
* actions
* summary
* datasources
* children
* preview
* widgets

{% code title="YAML order" %}
```yaml
title: Name
description: Description of your Jig
type: jig.default
icon: hold-balloon
badge: empty

inputs:
  name: 
    type: string
    
placeholders:
  - title: No data to display

onFocus: 
  type: action.sync-entities
  options:
    provider: DATA_PROVIDER_LOCAL
    entities:
      - entity: default/department

onRefresh: 
  type: action.sync-entities
  options:
    provider: DATA_PROVIDER_DYNAMIC
    entities:
      - default/employee

expressions: 
  ExpressionName: =@ctx.datasources.employee-data.email
  
header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://builder.jigx.com/assets/images/header.jpg

actions:
  - children:
      - type: action.go-back
        options:
          title: go back

summary:
  children:
    type: component.summary
    options: 
      layout: default
      
datasources:
  food: 
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
  
      entities:
        - default/employee
  
      query: SELECT id, '$.id', '$.name' FROM [default/employee] 

children:
  - type: component.avatar
    options:
      title: Jigx
      
preview:
  children:
    - type: component.web-view
      options:
        uri: https://jigx.com/
        
widgets:
  widget name: 
    type: widget.image
    options:
      source:
        uri: https://jigx.com/
```
{% endcode %}

### Order of items in a section

Order of items within a section, for example when defining a component we should aim to standardise as follows:

* Type is always the first thing to be defined so that we know what we are dealing with
* Meta elements for the list (data)
* Item definition
* Title
* Subtitle
* Description
* Left element , Right element , Label
* action
* OnPress
* Swipeable

{% code title="section-order" %}
```yaml
children:
  - type: component.list
    options:
      data: =@ctx.datasources.loads
      item:
        type: component.list-item
        options:
          title: Altitude
          subtitle: =@ctx.current.item.altitude
          description: =@ctx.current.item.altitude
          leftElement:
            element: avatar
            text: =$string(@ctx.current.item.loadNumber)
            uri: ''
          rightElement:
            element: value
            text: =$substring(@ctx.current.item.loadTime,0,5)
          label:
            title: =@ctx.current.item.loadStatus
            color: color1
            - when: =@ctx.current.item.loadStatus = 'Pending'
            color: color4
            - when: =@ctx.current.item.loadStatus= 'Accepted'
            color: color3
            - when: =@ctx.current.item.loadStatus = 'Completed'
            color: color2
            onPress:
            type: action.go-to
            options:
            linkTo: form-load
            parameters:
            loadid: =@ctx.current.item.id
            swipeable:
            right:
            - label: Delete
            icon: delete-2
            color: negative
              onPress:
              type: action.execute-entity
              options:
              provider: DATA_PROVIDER_DYNAMIC
              entity: default/load
                  method: delete
            data:
            id: =@ctx.current.item.id
```
{% endcode %}
