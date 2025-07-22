---
title: Inputs & outputs (Alpha)
slug: IAco-inputs
createdAt: Thu Nov 14 2024 14:01:57 GMT+0000 (Coordinated Universal Time)
updatedAt: Tue Feb 04 2025 14:30:52 GMT+0000 (Coordinated Universal Time)
---

:::hint{type="danger"}
This feature is currently in its **Alpha** stage of development.

- As an early version, it may not include all planned functionalities and is subject to significant changes based on ongoing development and user feedback.
- In this phase, the feature may contain bugs or behave unpredictably.
- Jigx recommends using standard, fully supported components until this feature has been fully tested and refined.
- We encourage you to provide feedback and report any issues to help us improve and refine the feature for future releases.

  :::

Use inputs and outputs to transfer and read data in custom components. This approach lets you configure a component once and reuse it across multiple screens or even on the same screen. By simply defining different inputs and outputs each time the component is used, you can display varied data and adapt to different contexts effortlessly.

## Inputs

Define `inputs` in the custom component, then in the jig using the custom component, provide the data/context for the input, either referencing a datasource or adding values.

### Examples and code snippets

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
In this example, we create a tab component using the `view` and `text` custom components. By leveraging inputs, the tab component can be reused within the same jig. The first tab component is center-aligned with four tabs, while the second is left-aligned with three tabs. Tab names for each component are dynamically set using the `tabName` input.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-vgBlOVBWz2M6muoG9AR7S-20241121-074013.png" size="70" position="center" caption="Tabs using inputs" alt="Tabs using inputs"}
:::
::::

For more examples using inputs, see the following:

|                                                                                                |                                                                                               |                                                                                              |
| ---------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| [Cards in a list](https://docs.jigx.com/examples/card-alpha#C6fgj)                             | [Ratings](https://docs.jigx.com/examples/combine-custom-and-standard-components-alpha#sgMBJ)  | [Tags](https://docs.jigx.com/examples/combine-custom-and-standard-components-alpha#ny3qM)    |
| [Cards with charts](https://docs.jigx.com/examples/card-alpha#6_eE4)                           | [Sections](https://docs.jigx.com/examples/combine-custom-and-standard-components-alpha#sQJ4v) | [Toggles](https://docs.jigx.com/examples/combine-custom-and-standard-components-alpha#BM6V-) |
| [Countdown](https://docs.jigx.com/examples/combine-custom-and-standard-components-alpha#iIk03) | [Stepper](https://docs.jigx.com/examples/combine-custom-and-standard-components-alpha#PbExW)  |                                                                                              |

:::CodeblockTabs
custom-component.jigx

```yaml
# components/media-types.jigx
type: component.default
# Inputs determine the name, alignment, indicator and value of the tabs
inputs:
  # inputs for indicators
  tabIndicator1:
    required: false
    type: boolean
  tabIndicator2:
    required: false
    type: boolean
  tabIndicator3:
    required: false
    type: boolean
  tabIndicator4:
    required: false
    type: boolean
  # inputs for tab names
  tabName1:
    required: true
    type: string
  tabName2:
    required: true
    type: string
  tabName3:
    required: false
    type: string
  tabName4:
    required: false
    type: string
  # inputs for tab values
  tabValue1:
    required: true
    type: string
  tabValue2:
    required: true
    type: string
  tabValue3:
    required: false
    type: string
  tabValue4:
    required: false
    type: string
  # input to determine alignment of the tab, e.g. center, left, right.
  tabsAlignment:
    required: false
    type: string

children:
  # There are 4 tabs configured in this custom component.
  # Using the view component creates the layout for the tabs
  # Tab 1
  - type: component.view
    options:
      style:
        border:
          bottom:
            style: solid
        flex:
          direction: row
          grow: 1
        justifyContent: center
        margin:
          vertical: medium
      children:
        - type: component.view
          when: =@ctx.inputs.tabValue1 != null
          options:
            style:
              flex:
                direction: row
                grow: =@ctx.inputs.stretchTabs = true ? 1:0
              gap: minimal
              padding:
                left: =@ctx.inputs.tabsAlignment = "center" ? "medium":"none"
                right: =@ctx.inputs.tabsAlignment = "center" ? "medium":"large"

            children:
              - type: component.view
                options:
                  style:
                    gap: medium
                  children:
                    - type: component.view
                      options:
                        style:
                          alignItems: center
                          flex:
                            direction: row
                          gap: minimal
                          justifyContent: center
                        # Using the text component to configure the tab text
                        children:
                          - type: component.text
                            options:
                              emphasis: =@ctx.solution.state.tab = @ctx.inputs.tabValue1 ? "":"medium"
                              value: =@ctx.inputs.tabName1
                              weight: bold

                    - type: component.view
                      options:
                        children: []
                        style:
                          background:
                            color:
                              =@ctx.solution.state.tab = @ctx.inputs.tabValue1 ?
                              "element":"transparent"
                          flex:
                            grow: 1
                          height: 2

              - type: component.view
                when: =@ctx.inputs.tabIndicator1 = true
                options:
                  style:
                    flex:
                      grow: 1
                  children:
                    - type: component.view
                      options:
                        children: []
                        style:
                          background:
                            color: negative
                          height: 6
                          radius: large
                          width: 6
            # Configure the onPress event to show the content in tab 1 when it is pressed.
            onPress:
              type: action.set-state
              options:
                state: =@ctx.solution.state.tab
                value: =@ctx.inputs.tabValue1
        # Tab 2
        # Using the view component creates the layout for the tabs
        - type: component.view
          when: =@ctx.inputs.tabValue2 != null
          options:
            style:
              flex:
                direction: row
              gap: minimal
              padding:
                left: =@ctx.inputs.tabsAlignment = "center" ? "medium":"none"
                right: =@ctx.inputs.tabsAlignment = "center" ? "medium":"large"

            children:
              - type: component.view
                options:
                  style:
                    gap: medium
                  children:
                    - type: component.view
                      options:
                        style:
                          alignItems: center
                          flex:
                            direction: row
                          gap: minimal
                          justifyContent: center

                        children:
                          - type: component.text
                            options:
                              emphasis: =@ctx.solution.state.tab = @ctx.inputs.tabValue2 ? "":"medium"
                              value: =@ctx.inputs.tabName2
                              weight: bold

                    - type: component.view
                      options:
                        children: []
                        style:
                          background:
                            color:
                              =@ctx.solution.state.tab = @ctx.inputs.tabValue2 ?
                              "element":"transparent"
                          flex:
                            grow: 1
                          height: 2

              - type: component.view
                when: =@ctx.inputs.tabIndicator2 = true
                options:
                  style:
                    flex:
                      grow: 1
                  children:
                    - type: component.view
                      options:
                        children: []
                        style:
                          background:
                            color: negative
                          height: 6
                          radius: large
                          width: 6
            # Configure the onPress event to show the content in tab 2 when it is pressed.
            onPress:
              type: action.set-state
              options:
                state: =@ctx.solution.state.tab
                value: =@ctx.inputs.tabValue2
        # Tab 3
        # Using the view component creates the layout for the tabs
        - type: component.view
          when: =@ctx.inputs.tabValue3 != null
          options:
            style:
              flex:
                direction: row
              gap: minimal
              padding:
                left: =@ctx.inputs.tabsAlignment = "center" ? "medium":"none"
                right: =@ctx.inputs.tabsAlignment = "center" ? "medium":"large"

            children:
              - type: component.view
                options:
                  style:
                    gap: medium
                  children:
                    - type: component.view
                      options:
                        style:
                          alignItems: center
                          flex:
                            direction: row
                          gap: minimal
                          justifyContent: center

                        children:
                          - type: component.text
                            options:
                              emphasis: =@ctx.solution.state.tab = @ctx.inputs.tabValue3 ? "":"medium"
                              value: =@ctx.inputs.tabName3
                              weight: bold

                    - type: component.view
                      options:
                        children: []
                        style:
                          background:
                            color:
                              =@ctx.solution.state.tab = @ctx.inputs.tabValue3 ?
                              "element":"transparent"
                          flex:
                            grow: 1
                          height: 2

              - type: component.view
                when: =@ctx.inputs.tabIndicator3 = true
                options:
                  style:
                    flex:
                      grow: 1

                  children:
                    - type: component.view
                      options:
                        children: []
                        style:
                          background:
                            color: negative
                          height: 6
                          radius: large
                          width: 6
            # Configure the onPress event to show the content in tab 3 when it is pressed.
            onPress:
              options:
                state: =@ctx.solution.state.tab
                value: =@ctx.inputs.tabValue3
              type: action.set-state
        # Tab 4
        # Using the view component creates the layout for the tabs
        - type: component.view
          when: =@ctx.inputs.tabValue4 != null
          options:
            style:
              flex:
                direction: row
              gap: minimal
              padding:
                left: =@ctx.inputs.tabsAlignment = "center" ? "medium":"none"
                right: =@ctx.inputs.tabsAlignment = "center" ? "medium":"large"

            children:
              - type: component.view
                options:
                  style:
                    gap: medium

                  children:
                    - type: component.view
                      options:
                        style:
                          alignItems: center
                          flex:
                            direction: row
                          gap: minimal
                          justifyContent: center

                        children:
                          - type: component.text
                            options:
                              emphasis: =@ctx.solution.state.tab = @ctx.inputs.tabValue4 ? "":"medium"
                              value: =@ctx.inputs.tabName4
                              weight: bold

                    - type: component.view
                      options:
                        children: []
                        style:
                          background:
                            color:
                              =@ctx.solution.state.tab = @ctx.inputs.tabValue4 ?
                              "element":"transparent"
                          flex:
                            grow: 1
                          height: 2

              - type: component.view
                when: =@ctx.inputs.tabIndicator4 = true
                options:
                  style:
                    flex:
                      grow: 1
                  children:
                    - type: component.view
                      options:
                        children: []
                        style:
                          background:
                            color: negative
                          height: 6
                          radius: large
                          width: 6
            # Configure the onPress event to show the content in tab 4 when it is pressed.
            onPress:
              type: action.set-state
              options:
                state: =@ctx.solution.state.tab
                value: =@ctx.inputs.tabValue4
```

jig.jigx

```yaml
# jigs/media.jigx
title: Media
type: jig.default
icon: app-window-four

children:
  - type: component.section
    options:
      title: Static tabs - Center Align
      children:
        # Inputs are used to determine the tab name, value, alignment and indicator.
        # First set of tabs.
        - type: component.custom-component
          componentId: tabs
          inputs:
            tabIndicator1: false
            tabIndicator2: true
            tabIndicator3: true
            tabIndicator4: true
            tabName1: Tab 1
            tabName2: Tab 2
            tabName3: Tab 3
            tabName4: Tab 4
            tabValue1: tab1
            tabValue2: tab2
            tabValue3: tab3
            tabValue4: tab4
            tabsAlignment: center

  - type: component.section
    options:
      title: Static tabs - Left Align
      children:
        # Same custom component reused as above using the view component.
        # Using inputs you can change the appearance of the same custom component.
        # Second set of tabs.
        - type: component.custom-component
          componentId: tabs
          inputs:
            tabIndicator1: true
            tabIndicator2: true
            tabIndicator3: false
            tabIndicator4: true
            tabName1: Dashboard
            tabName2: Requests
            tabName3: Orders
            tabValue1: tab1
            tabValue2: tab2
            tabValue3: tab3
```

:::

## Outputs

- The `output` and `input` work in conjunction with each other.
- Define `outputs` in the custom component, then in the jig using the custom component, provide the data/context (`input`) by referencing the custom-component `instanceId`.
- An `instanceId` is required for the custom component that is exposing an `output` in order to access the output via `state`.
- The `output` requires an `output-key` and a data value that is available in the custom component.
- Accessing `outputs` uses the format similar to:
  `=@ctx.components.[instanceId].outputs.output-key`. Use IntelliSense to assist with configuration.

### Examples and code snippets

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
In this simple example, the custom component is configured with a `form` in a `card` component. An `output` property is added to the custom component. This allows for the data entered into the custom component's `form` on the jig to be transferred to the `title` property of the `image` component on the jig.

:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-pfCa1E190iHeoJJ2auptm-20241118-135414.gif" size="56" position="center" caption="Output data to image label" alt="Output data to image label"}
:::
::::

:::CodeblockTabs
custom-component

```yaml
type: component.default
componentId: brand-form

# Configure the output value to be accessible outside of the custom component.
outputs:
  brand-label: =@ctx.components.company-name.state.value

children:
  - type: component.card
    options:
      children:
        - type: component.form
          instanceId: new-form
          options:
            children:
              - type: component.text-field
                instanceId: company-name
                options:
                  label: Company Name
```

jig.jigx

```yaml
title: Jars of health
description: Label your favorite jar
type: jig.default

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1490072760529-d4c88a565a38?w=800&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTJ8fGphciUyMHNob3B8ZW58MHx8MHx8fDA%3D

children:
  - type: component.custom-component
    componentId: brand-form
    # InstanceId should be supplied in order to access the state of the output.
    instanceId: jigx-form

  - type: component.image
    options:
      # The value entered in the custom component,
      # will be transferred to the title field on the image.
      title: =@ctx.components.jigx-form.outputs.button-title
      source:
        uri: https://images.unsplash.com/photo-1691480208637-6ed63aac6694?w=800&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8N3x8YmxhbmslMjBsYWJlbHxlbnwwfHwwfHx8MA%3D%3D
```

:::

### See also

- [Passing data using inputs](<./../Jigs _screens_/Passing data using inputs.md>)
- [Passing data using outputs](<./../Jigs _screens_/Passing data using outputs.md>)
