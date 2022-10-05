---
layout: layouts/post.njk
title: Custom Connector Conundrums
date: 2022-10-05T17:41:29.152Z
tags:
  - blog
  - flow
  - power-automate
  - canvas-app
  - custom-connector
---
Requirement: Create a Custom Connector for D365 F&O

I﻿ recently had a requirement to create a custom connector and was provided a Postman collection to help me along my way. I imported this collection into Postman and found that it contained two endpoints:

1.





![](/images/generic_oauth_2.png "Generic OAuth 2.0 Authorization Flow")

I was following along with the documentation, [Create a custom connector from a Postman collection](https://learn.microsoft.com/en-us/connectors/custom-connectors/define-postman-collection#import-the-postman-collection-for-power-automate-and-power-apps) and having no issues until I came