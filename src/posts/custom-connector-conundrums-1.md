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
  - oauth-2.0
---
Requirement: Create a Custom Connector for D365 F&O

I﻿ recently had a requirement to create a custom connector and was provided a Postman collection to help me along my way. I imported this collection into Postman and found that it contained two endpoints - one of which was an authorization code flow

```json
{
    "token_type": "Bearer",
    "expires_in": "3599",
    "ext_expires_in": "3599",
    "expires_on": "1664997070",
    "not_before": "1664993170",
    "resource": "https://*********************************.axcloud.dynamics.com",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6IjJaUXBKM1VwYmpBWVhZR2FYRUpsOGxWMFRPSSIsImtpZCI6IjJaUXBKM1VwYmpBWVhZR2FYRUpsOGxWMFRPSSJ9.eyJhdWQiOiJodHRwczovL2F6d2RldmRmbmMwMzRmYzVhYTJmYjZlYjMzOGFkZXZhb3MuYXhjbG91ZC5keW5hbWljcy5jb20iLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC84MzRmYjdiNC02MjRkLTRkZTgtYTk3Ny0yZDQ2YWQ5NzliZDkvIiwiaWF0IjoxNjY0OTkzMTcwLCJuYmYiOjE2NjQ5OTMxNzAsImV4cCI6MTY2NDk5NzA3MCwiYWlvIjoiRTJaZ1lQaHA4bmlYTmZ2OUcySzNXMkxVeTE1bkFBQT0iLCJhcHBpZCI6IjkxMzUxY2ZjLTllMjYtNDg2OS04MWNlLWRkMDdhNGI1ZjU4MSIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzgzNGZiN2I0LTYyNGQtNGRlOC1hOTc3LTJkNDZhZDk3OWJkOS8iLCJvaWQiOiI1OTFlNmQ3MS1lYmViLTQ5ODItOGFhOC0xZGE2OTQ2MjFkMzIiLCJyaCI6IjAuQVhRQXRMZFBnMDFpNkUycGR5MUdyWmViMlJVQUFBQUFBQUFBd0FBQUFBQUFBQUIwQUFBLiIsInN1YiI6IjU5MWU2ZDcxLWViZWItNDk4Mi04YWE4LTFkYTY5NDYyMWQzMiIsInRpZCI6IjgzNGZiN2I0LTYyNGQtNGRlOC1hOTc3LTJkNDZhZDk3OWJkOSIsInV0aSI6IklJVFc4U2hhT1VhSndnN3dsc1JuQUEiLCJ2ZXIiOiIxLjAifQ.s-sdF0mynn9WEaJg3qzD-Jby8UZV58OpCr1KLq8Z4mBXSpzfVNBvDqEDBHjgS89TxjjiePBLW29W32QkYJ46c1wiYKEHZ_i6YBLiyjPf2l4ng2TY7Bs9NJi_-TrDbNLRpZgS7gq5k_W4JK_vvcAEEAL11gIULpePKQ3zESyQ18GulDnu5s_DR8iRv0LK7kCiVCyKrUh_vQB6W8Gi33YL5v8V0A_ixDX0FmwGURlz1VWU8ZrTViLyIt57UDaU14ixur1h4Nmj9jWfLbd_RJoPd4I3z6u8ptwR4fITCln8x8ixeJnufbzS6V0g0bDMGCAR_P7Xj1qtBTTKoVJultv-Hg"
}
```



![](/images/generic_oauth_2.png "Generic OAuth 2.0 Authorization Flow")

I was following along with the documentation, [Create a custom connector from a Postman collection](https://learn.microsoft.com/en-us/connectors/custom-connectors/define-postman-collection#import-the-postman-collection-for-power-automate-and-power-apps) and having no issues until I came