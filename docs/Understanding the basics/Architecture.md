---
title: Architecture
slug: Brca-jigx
description: Understanding the Jigx platform 
createdAt: Fri Apr 21 2023 14:29:27 GMT+0000 (Coordinated Universal Time)
updatedAt: Thu Jan 09 2025 07:10:07 GMT+0000 (Coordinated Universal Time)
---

The Jigx platform consists of components that work together enabling you to build enterprise mobile app solutions.

![Jigx Overview](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/3rJSBLdbOOKqiFIX8diTO_jigxoverview.png "Jigx Overview")

| Component                                                                    | Description                                                                                                                                                                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Jigx Builder](<./../Building Apps with Jigx/Jigx Builder _code editor_.md>) | The Jigx Builder is an extension in Microsoft VS Code, a development environment that can be installed on many platforms, including Windows and Mac. Use YAML, SQL, JSON, and JSONata to build, test, debug, and publish Jigx mobile apps.                                                                                                                          |
| Jigx Cloud                                                                   | JigxCloud authenticates users, stores organizations and solutions, and sends notifications.                                                                                                                                                                                                                                                                                  |
| [Jigx Management](<./../Administration/Management Overview.md>)              | Jigx Management exposes the Jigx Cloud functionality in a browser-based portal, allowing you to manage users and solutions, set up send and push notifications, and view usage metrics of your organization.                                                                                                                                                                 |
| Jigx App                                                                     | The Jigx App is an iOS and Android app that works on mobile devices such as phones and tablets. The app is available in the iOS and Google Play stores. Jigx solutions built-in Jigx Builder, published to Jigx Cloud and permissions granted in Jigx Management are accessible in the Jigx App. The Jigx App is only supported in portrait mode on iOS and Android phones.  |
| [Data](<./../Building Apps with Jigx/Data.md>)                               | Understanding how data is used and how it flows between the Jigx components is important. Jigx data concepts, including data lifecycles, syncing and loading data, and how to work with REST, Azure SQL, and Dynamic Data are covered in the [Data](<./../Building Apps with Jigx/Data.md>) topic.                                                                           |

### See Also

- [REST Authentication](<./../Building Apps with Jigx/Data/Data Providers/REST/REST Authentication.md>)
- [Local REST Calls](<./../Building Apps with Jigx/Data/Data Providers/REST/Local REST Calls.md>)
