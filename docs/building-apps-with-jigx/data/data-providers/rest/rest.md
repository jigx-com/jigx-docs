---
layout:
  width: wide
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
---

# REST

This section explains how to configure the REST data provider to call external REST API endpoints. Use it to fetch data, send updates, or trigger external services in response to user interaction. The REST data provider is one of the most commonly used in Jigx solutions, enabling data exchange with REST services that accept or return JSON, XML, or binary data.

## REST Data Provider Architecture

When a REST call returns data to Jigx, the processed format, such as JSON, is inserted into a local SQLite database. The Jigx mobile application then queries the database, displaying the data on the device. This architecture supports offline scenarios. Data is stored in a document database format. Jigx provides a shorthand SQL parser to select using logical column names. Alternatively, you can use the native json\_extract() function to manipulate the data from SQLite. When the result of the output transform is an array of JSON objects, Jigx will insert each item in the array in its row. Note that SQL is case-insensitive while JSON is case-sensitive.

{% embed url="https://vimeo.com/848055698" %}

## Examples and code snippets

The following examples with code snippets are provided:

<table><thead><tr><th width="130.22265625">Example</th><th></th></tr></thead><tbody><tr><td><a href="https://docs.jigx.com/examples/readme/data-providers/rest/create-an-app-using-rest-apis">Hello REST</a></td><td>In this section, a REST API is used to create a customers Jigx app, allowing you to add new customers and update and view customer details, location, and images.</td></tr><tr><td><a href="https://docs.jigx.com/examples/readme/data-providers/rest/ms-graph">MS Graph</a></td><td>The MS Graph examples use the User, Calendar, Mail, Insights, and To-do tasks to create a powerful Jigx apps with everything you need in one app.</td></tr></tbody></table>

## Building a REST based app video resources

{% columns %}
{% column %}
{% embed url="https://vimeo.com/848412406?fe=sh&fl=pl" %}

1. Introduction to REST API\
   6:59 min
{% endcolumn %}

{% column %}
{% embed url="https://vimeo.com/848059289?fe=sh&fl=pl" %}

2. Exploring REST and JSONata 6:17 min
{% endcolumn %}
{% endcolumns %}

{% columns %}
{% column %}
{% embed url="https://vimeo.com/848062137?fe=sh&fl=pl" %}

3. Building a REST based App\
   9:14 min
{% endcolumn %}

{% column %}

{% endcolumn %}
{% endcolumns %}
