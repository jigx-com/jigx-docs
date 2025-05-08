---
title: Passing data using inputs
slug: Uwuu-passing-data
createdAt: Thu Jan 11 2024 09:44:23 GMT+0000 (Coordinated Universal Time)
updatedAt: Tue Nov 05 2024 11:25:46 GMT+0000 (Coordinated Universal Time)
---

Often, you need to transfer or pass data between jigs to provide context and data, for example, when pressing on a customer in a list, the customer ID is passed to the order form, pre-populating the customer's details. This is accomplished by utilizing inputs and [outputs](<./Passing data using outputs.md>).

## Inputs

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-G14iv57uCn5sJjTkM10Ub-20240730-091942.png" size="50" position="center" caption="Passing data using inputs" alt="Passing data using inputs"}

The input data is configured in one of the following:

- In the index.jigx file under each jig's `input` property.
- In another jig under the `parameters` property.

You can define the following for inputs:

- The data type
- Whether the input is required or not
- A default value if no input is provided.

## Configuration options

| **Properties** | **Values**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `default`      | Add a value that will display as the default if nothing is specified. This property is optional.                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `required`     | - `true` - a value for the input is required
- `false` - value is optional; if no value is specified, the default value is shown if provided; otherwise, the input value is empty.                                                                                                                                                                                                                                                                                                                                                                                     |
| `type`         | `string` - input must be of type string, for example, Mary.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|                | `object` - input must be an object with properties defined. <br />- The full object can be returned using `=@ctx.jig.inputs.object`
- Individual properties can be returned using `=@ctx.jig.inputs.object.property`                                                                                                                                                                                                                                                                                                                                                   |
|                | `array` - input must be an array.<br />- The full array can be returned using `=@ctx.jig.inputs.array`
- Single elements in an array can be returned using `=@ctx.jig.inputs.array.element`
- Individual items in an array can be returned using `=@ctx.jig.inputs.array[1].element`<br />The YAML format for specifying the array can be one of the following:<br />- `array: [{name: John, age: 30}, {name: Melany, age: 35}, {name: Scott, age: 21}]`
- `array:    - [John, Melany, Mel, 1234, true]`
- `array:    - John    - Melany    - Mel    - 1234    - true` |
|                | `boolean` - input must be `true` or `false`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|                | `number` - input must be of type number, for example, 45 or 350.88.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |

:::::ExpandableHeading
### YAML code for index.jigx to jig

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
**Index.jigx:**
In the index.jigx file configure the input under the widget configuration for the jig.  Configure the data you want to pass to that jig.
Example:
`size: "1x1"`
`jigId: application-form`
`inputs:`
` name: =@ctx.user.displayName`
:::

:::VerticalSplitItem
**Input:**
In the receiving jig configure the input type and specify the data in the field or data property using an expression.

Example of the *input type*:
`inputs:
  name: 
    default: Placeholder
    type: string
    required: true`

Example of an *input expression*:
`title: =@ctx.jig.inputs.name`
:::
::::
:::::

:::::ExpandableHeading
### YAML code for jig to jig

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
**Parameter:**
In the jig containing the data you want to transfer, and configure the various parameters to be passed.
Example:
`parameters: `
`   packageDate: =@ctx.current.item.date
 `    `packageName: =@ctx.current.item.name`
:::

:::VerticalSplitItem
**Input:**
In the receiving jig configure the component to recieve the data from the parameter.
Example:
`title: =@ctx.jig.inputs.packageName`
:::
::::
:::::

## Considerations

- You can specify a default value that can be used as a placeholder if no input value is found in the configuration. Use the `default` property when defining the input types.
- With inputs, `parameters` are configured in the first jig (sending jig) with the `input` used in the receiving jig.
- The `parameter` and `input` work in conjunction with each other.
- The `parameter` requires a `parameterName` and a data value that is available in that jig.
- Multiple `parameters` can be passed through at once.
- The receiving jig configuration uses the format `=@ctx.jig.inputs.parameterName`. Use IntelliSense (ctrl+space) to assist with configuration.
- In a jig, you can access all data sent from other jigs using the expression `@ctx.jig.inputs.[parameter]`, for example, `=@ctx.datasources.contacts[customerId = @ctx.jig.inputs.customerId]`
- Inputs can be used for passing values from a [composite]() jig to its children jigs.
- If you are in a list-item component, you don't need to list all the parameters, simply use:
  `parameters:                     
      customer: =@ctx.current.item`

## Examples

### Passing data directly from index.jigx to a jig

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
Jig input definitions are configured directly in the jig and the input values are defined in the index.jigx file. The values from the index file are directly returned to the jig.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/0jTAXb6d8XmPInsrVw87s_inputsdefinition.PNG" size="88" position="center" caption="Input definitions" alt="Input definitions"}
:::
::::

:::CodeblockTabs
jig-inputs-direct.jigx

```yaml
title: Jig input defintions
description: Inputs directly received from index.jigx 
type: jig.default

header:
  type: component.jig-header
  options:
    height: medium
    children: 
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1516542076529-1ea3854896f2?q=80&w=1742&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
# Add the jig's input defintion to the jig file
inputs:
  name: 
    type: string
    required: true
  alternate-name: 
    default: Placeholder
    required: false
    type: string
  number:
    type: number
  boolean:
    type: boolean
    required: true
  array: 
    type: array
    required: true
  object:
    type: object
    properties:
      obj-name: 
        type: string
      obj-age:
        type: number
      obj-member: 
        type: boolean
             
children:
  - type: component.entity
    options:
      isCompact: true
      children:
        - type: component.entity-field
          options:
            label: Name (string)
        # Reference the input using the inputs name   
            value: =@ctx.jig.inputs.name
        - type: component.entity-field
          options:
            label: Alternate Name (string-default)
        # Reference the input using the inputs name
        # No input is added in index.jigx so the default is shown 
            value: =@ctx.jig.inputs.alternate-name
        - type: component.entity-field
          options:
            label: contact number (number)
        # Reference the input using the inputs name    
            value: =@ctx.jig.inputs.number
        - type: component.entity-field
          options:
            label: Member (Boolean)
        # Reference the input using the inputs name    
            value: =@ctx.jig.inputs.boolean
        - type: component.entity-field
          options:
            label: Other members (array)
        # Reference the input using the inputs name
        # Specify the elements in the array to be returned
        # In this instance it is name
        # In the expression specific the item must be a string    
            value: =$string(@ctx.jig.inputs.array.name)
        - type: component.entity-field
          options:
            label: Other members (array-item)
        # Reference the input using the inputs name 
        # Specify the element in the array to be returned
        # Specify that only one item in the array must be returned
        # In this instance it is name       
            value: =@ctx.jig.inputs.array[1].name    
        - type: component.entity-field
          options:
            label: Object
        # Reference the input using the inputs name 
        # Specify the object to be returned
        # All parameters in the object are returned 
            value: =$string(@ctx.jig.inputs.object)
        - type: component.entity-field
          options:
            label: Name (object)
        # Reference the input using the inputs name 
        # Specify the one parameter in the object to be returned
        # All parameters in the object are returned
        # In this instance the name parameter    
            value: =@ctx.jig.inputs.object.obj-name
        - type: component.entity-field
          options:
            label: Age (object)
        # Reference the input using the inputs name 
        # Specify the one parameter inthe object to be returned
        # All parameters in the object are returned
        # In this instance the age parameter       
            value: =@ctx.jig.inputs.object.obj-age
        - type: component.entity-field
          options:
            label: Member (Object)
        # Reference the input using the inputs name 
        # Specify the one parameter in the object to be returned
        # All parameters in the object are returned
        # In this instance the member parameter       
            value: =@ctx.jig.inputs.object.obj-member   
```

index.jigx

```yaml
name: simple-list
title: simple-list
category: business         

widgets:
# Add inputs
  - size: "1x1"
    jigId: new-input
    inputs:
      name: =@ctx.user.displayName
      number: 350
      boolean: true
    # The array can be in the following YAML format - option 1
      array: [{name: john, age: 30}, {name: melany, age: 35}, {name: scott, age: 21}]
    # Array YAML format - option 2
        # - [john, melany, mel, 1234, true]
    # Array YAML format - option 3 
        # - john
        # - melany
        # - mel
        # - 1234
        # - true
      object: 
        obj-name: Gigi
        obj-age: 50
        obj-member: false
```
:::

### Dynamically pass data from another jig's components

Jig input definitions are configured directly in the jig and the input values returned from components configured in another jig. In the example below a form captures the student details, the *Student Details* form links to the *Student Card* jig and uses parameters to pass the values required in the *Student Card* inputs.

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/26_CwRD8Y7MD_092ze_1K_inputscard.PNG" size="70" position="center" caption="Dynamic input" alt="Dynamic input"}

:::CodeblockTabs
input-student-card.jigx

```yaml
title: Student Card
type: jig.default
# Define inputs for the jig
inputs:  
  studentName: 
    type: string
    required: true
  studentContact:
    type: number
    required: true
  studentAddress: 
    type: object
    required: false   
  studentPhoto: 
    type: string
    required: true
  studentAllergies:
    type: array
    required: true
  studentResident: 
    type: boolean
    required: true
    default: false
    
children:
   - type: component.card
     options:
       color: color9
       children:
        - type: component.avatar
          options:
            align: center
            size: large
            title: =@ctx.jig.inputs.studentName
            uri: =@ctx.jig.inputs.studentPhoto
        
        - type: component.entity
          options:
            isCompact: true
            children:
               - type: component.entity-field
                 options:
                  label: Name
                  value: =@ctx.jig.inputs.studentName
               - type: component.entity-field
                 options:
                    label: Contact number
                    value: =@ctx.jig.inputs.studentContact
               - type: component.entity-field
                 options:
                  label: Address
                  value: =(@ctx.jig.inputs.studentAddress.streetAddress & ', ' & @ctx.jig.inputs.studentAddress.cityAddress & ', ' & @ctx.jig.inputs.studentAddress.countryAddress)
               - type: component.field-row
                 options:
                   children:
                     - type: component.entity-field
                       options:
                         label: Residence
                         value: =@ctx.jig.inputs.studentResident
                     - type: component.entity-field
                       options:
                         label: Allergies
                         value: =$string(@ctx.jig.inputs.studentAllergies.allergen)
```

input-student-details.jigx

```yaml
title: Student Details
description: The values captured in the form are used as the input to create a student card jig
type: jig.default

header:
  type: component.jig-header
  options:
    height: medium
    children: 
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1541339907198-e08756dedf3f?q=80&w=2970&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D    

datasources:
  allergies: 
    type: datasource.static
    options:
      data:
        - id: 1
          allergen: none
          icon: smiley-happy
        - id: 2
          allergen: nuts
          icon: food-allergic-peanut-2
        - id: 3
          allergen: shellfish
          icon: shellfish-lobster
        - id: 4
          allergen: milk
          icon: food-allergic-daily-milk-product-3
        - id: 5
          allergen: eggs
          icon: animal-products-eggs
        - id: 6
          allergen: wheat   
          icon: food-allergic-gluten-2   
  
children:
  - type: component.section
    options:
      title: Student Details
      children: 
        - type: component.form
          instanceId: inputValues
          options:
            children:
              - type: component.text-field
                instanceId: firstName
                options:
                  label: Fist name
                  isRequired: false
              - type: component.email-field
                instanceId: email
                options:
                  label: Email address
              - type: component.number-field
                instanceId: phoneNumber
                options:
                  label: Mobile number
              - type: component.checkbox
                instanceId: resident
                options:
                  label: Are you in a residence hall?
                  isRequired: false
                  isOptionalLabelHidden: true
                
              - type: component.dropdown
                instanceId: studentAllergies
                options:
                  isMultiple: true
                  label: Do you have any allergies?
                  data: =@ctx.datasources.allergies
                  item:
                    type: component.dropdown-item
                    options:
                      leftElement: 
                        element: icon
                        icon: =@ctx.current.item.icon
                      title: =@ctx.current.item.allergen
                      value: =@ctx.current.item.allergen
             
  - type: component.section
    options:
      title: Personal Details
      children:
        - type: component.form
          instanceId: personalDetails
          options:
            children:
              - type: component.text-field
                instanceId: streetAddress
                options:
                  label: Street address
              - type: component.text-field
                instanceId: cityAddress
                options:
                  label: City
              - type: component.text-field
                instanceId: countryAddress
                options:
                  label: Country   
              - type: component.media-field
                instanceId: sutdentPhoto
                options:
                  label: Selfie
                  mediaType: image
actions:
  - children:
      - type: action.go-to
        options:
          title: Create card
          linkTo: input-student-card
          parameters:
            studentName: =@ctx.components.firstName.state.value
            studentContact: =@ctx.components.phoneNumber.state.value
            studentAddress: =@ctx.components.personalDetails.state.data
            studentPhoto: =@ctx.components.sutdentPhoto.state.value
            studentAllergies: =@ctx.components.studentAllergies.state.selected
            studentResident: =@ctx.components.resident.state.value
             
```
:::

:::::ExpandableHeading
### Passing data from one jig to another

In this example, the **sending** jig list called* Island Holiday Packages* is configured with `parameters` for the package date, price, and time. When tapping on a specific package, the parameters are sent to the **receiving** jig that uses the `inputs` in the `title` property to show the selected package, the date is used in the `expiresAt` property for the countdown component that counts down to the date, and the price is used in the action `title` displayed on the buy package button at the bottom of the screen.

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/gvf-nua3j_IavddFgHXJg_inputex1.png" size="58" position="center" caption="Sending and receiving jig" alt="Sending and receiving jig"}

**Sending Jig**

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/SW5CK3E82Zy0G78Ysw7Qd_inputsend.png" size="64" position="center" caption="Sending jig with parameters" alt="Sending jig with parameters"}
:::

:::VerticalSplitItem
Create a `jig.list` with `list.items` for the name, description of the holiday package and add a `rightElement: button` for the date with an `onPress` action. Then add parameters:
`packageName`, `packageDate`, and `packagePrice`. Add an expression for each similiar to `=@ctx.current.item.date`


:::
::::

:::CodeblockTabs
Holiday-packages.jigx

```yaml
title: Island Holiday Packages
type: jig.list

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1440778303588-435521a205bc?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8M3x8aG9saWRheXxlbnwwfHwwfHx8MA%3D%3D&auto=format&fit=crop&w=500&q=60
# Static datasource 
# With the name, escription, date and price of each package          
datasources:
  packages:
    type: datasource.static
    options:
      data:
        - name: Thailand
          date: "2024-12-14"
          description: "10 days in luxury accomodation"
          Price: "$ 1500"
        - name: Phuket
          date: "2024-11-25"
          description: "7 days experience cultural activities"
          Price: "$ 1000"
        - name: Mauritius
          date: "2024-05-04"
          description: "8 days includes watersports"   
          Price: "$ 2350"
        - name: Bali
          date: "2024-09-20" 
          description: "15 days all-inclusive experience"
          Price: "$ 3760"
data: =@ctx.datasources.packages
item:
# List of all the available packages showing the name and description
  type: component.list-item
  options:
    title: =@ctx.current.item.name
    subtitle: =@ctx.current.item.description
# Right button showing the start date of the holiday    
    rightElement: 
      element: button
      title: =@ctx.current.item.date
# An action to press on the button and go to the next jig    
      onPress: 
        type: action.go-to
        options:
          linkTo: selected-package
# Define the parameters that are transfered to the next jig.        
          parameters:
            packageDate: =@ctx.current.item.date
            packagePrice: =@ctx.current.item.Price
            packageName: =@ctx.current.item.name
```
:::

**Receiving Jig**

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
Create a `jig.default` for the receiving jig. In the `title:` property configure the input using  =`@ctx.jig.inputs.packageName`, in the `component.countdown: expiresAt` property add the input expression `=@ctx.jig.inputs.packageDate` and in the `action-confirm: title` property add the input expression `=@ctx.jig.inputs.packagePrice & " - BUY"`.


:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/K2IFFPXPBK4xNsBUHJitq_inputrec.png" size="64" position="center" caption="Input- receiving jig" alt="Input- receiving jig"}
:::
::::

:::CodeblockTabs
selected-package.jigx

```yaml
# Use the parameter for package name as an input for the title 
title: =@ctx.jig.inputs.packageName
type: jig.default

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://plus.unsplash.com/premium_photo-1675989167596-915a77b361e5?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8ODN8fGhvbGlkYXl8ZW58MHx8MHx8fDA%3D&auto=format&fit=crop&w=500&q=60
        
children:                                
  - type: component.countdown
    options:
      size: extra-large
 # Use the packageDate parameter as the date to use in the countdown        
      expiresAt: =@ctx.jig.inputs.packageDate
      
actions:
  - children:
      - type: action.confirm
        options:
# Use the packagePrice parameter as an input
# This displays the cost of the package on the Buy button        
          title: =@ctx.jig.inputs.packagePrice & " - BUY"
          isConfirmedAutomatically: false
          onConfirmed: 
            type: action.go-back
          modal:
            title: Let the countdown begin!
```
:::
:::::

:::::ExpandableHeading
### Passing data from a jig to a composite jig&#x20;

In this example, three jigs contain various information for all customers, namely:

1. *customer-list.jigx* - A list of customers.
2. *customer-contact.jigx* - A list of the customer contact person.
3. *customer-orders.jigx* - A list of orders.

When you click on a customer in the list (1) shown on the left screen below, a new jig opens combining the details from contact (2) and orders (3) into one screen (composite jig), shown on the right screen below and filters the data to show the selected customer's details. The composite jig is called *customer-overview\.jigx*.

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/bH9ftLRMiw6zpPtfFMRsF_inputcompex.png" size="60" position="center" caption="Send and receiving jigs" alt="Send and receiving jigs"}

To achieve this configure the following:

1. Create the composite jig and include the `JigIds` for the *customer-contact.jigx* and *customer-orders.jigx*.
2. Add the `customerId` and `customerName` input values transfered from the `parameters` in the *customer-list.jigx* to the `jigId` properties for the *customer-contacts.jigx*; and add `customerId` to the `jigId` for the *customer-order.jigx*. The result is that only the selected customer's contact person and orders will display.
3. Add parameters to the customer list that include the `customerId` and `customerName`.


**Sending Jig**

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/opBbbMDRrtoVlQ4joaAWJ_custlist.png" size="64" position="center" caption="Sending Jig with paramaters" alt="Sending Jig with paramaters"}
:::

:::VerticalSplitItem
Create a list jig called *customer-list.jigx*, use the datasource to list customer names and ids. Add `parameters` for the `customerName` and `customerId`.
:::
::::

:::CodeblockTabs
customer-list.jigx

```yaml
title: Customer List
type: jig.list
icon: list

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1464618663641-bbdd760ae84a?q=80&w=2940&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
        title: Customer List
        
datasources:
  customers:
    type: datasource.static
    options:
      data:
        - customerId: 1
          name: Island shop
        - customerId: 2
          name: Sea Depot
        - customerId: 3
          name: Beach accessories

data: =@ctx.datasources.customers
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.name
    subtitle: "='Customer ID: ' & @ctx.current.item.customerId"
    rightElement: 
      element: button
      title: Contact
      onPress: 
        type: action.go-to
        options:
          linkTo: customer-overview
  # Add parameters to use as input values in the composite jig      
          parameters:
            customerId: =@ctx.current.item.customerId
            customerName: =@ctx.current.item.name

```
:::

**Supporting Jigs **

Create two basic list jigs one for *customer-contacts* and the other for the *customer-orders*.

1. For the `data` property in both jig s add the `customerId` as an input
   `data:  =@ctx.datasources.datasourcename[customerId = @ctx.jig.inputs.customerId]`. Define the input type as string under the `inputs` property.
2. In the *customer-contacts.jigx* also add the `customerName` as an input with the type string.

:::CodeblockTabs
customer-contacts.jigx

```yaml
title: Customer Contacts
type: jig.list

inputs:
  customerId: 
    type: string
    required: true
  customerName: 
    type: string
    required: true

datasources:
  contacts: 
    type: datasource.static
    options:
      data:
        - customerId: 1
          name: Jane Stevens
        - customerId: 1
          name: Jenny Smith
        - customerId: 2
          name: Mark Miller
        - customerId: 2
          name: Luke Meyer
        - customerId: 3
          name: Terry Anderson
        - customerId: 3
          name: Laura Peterson
          
data: =@ctx.datasources.contacts[customerId = @ctx.jig.inputs.customerId]
item: 
  type: component.list-item
  options:
    isContained: true
    title: =@ctx.current.item.name
    subtitle: =@ctx.jig.inputs.customerName
```

customer-orders.jigx

```yaml
title: Customer orders
type: jig.list

inputs:
  customerId: 
    type: string
    required: true
    
datasources:
  beachItems: 
    type: datasource.static
    options:
      data:
        - customerId: 1
          order: paddle-board
          amount: 4
          icon: paddle-board    
        - customerId: 1
          order: surf-board
          amount: 10
          icon: skiing-board-slide
        - customerId: 2
          order: wetsuit
          amount: 15
          icon: surfing
        - customerId: 2
          order: hat
          amount: 20
          icon: hat
        - customerId: 3
          order: umbrella
          amount: 7
          icon: rain-umbrella-sun
        - customerId: 3
          order: sandcastle bucket
          amount: 6
          icon: color-bucket

data: =@ctx.datasources.beachItems[customerId = @ctx.jig.inputs.customerId]
item: 
  type: component.list-item
  options:
    isContained: true
    title: =@ctx.current.item.order
    subtitle: =@ctx.current.item.order
    leftElement: 
      element: icon
      icon: =@ctx.current.item.icon
    rightElement: 
      element: value
      text: =@ctx.current.item.amount 
      
```
:::

**Receiving jig (composite)**

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/4oZdpEDCgu-uoV8U7Vprf_custcomp.png" size="64" position="center" caption="Receiving composite Jig" alt="Receiving  composite Jig"}
:::

:::VerticalSplitItem
The receiving jig is a composite jig with two children *(customer-contacts* and *customer-orders*). In this example, we pass the `inputs` (*customerId* and *customerName*) to the children. The children can then access all `parameters` and render only the selected customers contact and order details.


:::
::::
:::::

:::CodeblockTabs
customer-overview\.jigx

```yaml
# Reference the customer name in the title
# Using the input from the parameter in the customer-list
title: ='Customer -' & @ctx.jig.inputs.customerName
type: jig.composite

# Specify the input's type and if the input is required or not
inputs:
  customerId: 
    type: string
    required: true
  customerName: 
    type: string
    required: true

header:
  type: component.jig-header
  options:
    height: small
    children:  
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1507525428034-b723cf961d3e?w=800&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8M3x8YmVhY2h8ZW58MHx8MHx8fDA%3D
      
children:
  - jigId: customer-contacts
# Reference the customerId & Name in the jigId 
# Using the input from the parameter in the customer-list
# Returns the contact person for the customer
    inputs:
      customerId: =@ctx.jig.inputs.customerId
      customerName: =@ctx.jig.inputs.customerName
  - jigId: customer-orders
# Reference the customerId in the jigId
# Using the input from the parameter in the customer-list
# Returns the orders for that customer
    inputs:
      customerId: =@ctx.jig.inputs.customerId
```
:::

