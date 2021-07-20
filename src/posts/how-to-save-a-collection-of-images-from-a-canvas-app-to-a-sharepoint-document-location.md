---
layout: layouts/post.njk
title: How to Save a Collection of Images from a Canvas App to a SharePoint
  Document Location
metaTitle: How to Save a Collection of Images from a Canvas App to a SharePoint
  Document Location
date: 2021-07-20T15:17:20.844Z
tags:
  - PowerApps
  - CanvasApp
  - SharePoint
  - Model-DrivenApp
  - DocumentLocations
---
I recently had a requirement for Field Service Engineers to be able to save multiple photos captured from the camera control in a Canvas App to the SharePoint Document Location associated with the Job record that they are working on - thereby giving the Administrators in the office full visibility of the photos from within the Model-Driven App that they use for scheduling the Jobs.

In order to achieve this I needed to configure:

1. The Model-Driven App; and
2. The Canvas App; and
3. A Power Automate Flow.

## The Model-Driven App

In terms of the Model-Driven app I needed to do two things:

1. Set the default document management settings via [Power Platform admin center](https://admin.powerplatform.microsoft.com/environments) > Your Environment > Settings > Integration > Document management settings:

![Document management settings](/images/dm_settings.png "Document management settings modal")

1. Add a related Documents Subgrid to the Main form of the Jobs table:

![Documents Subgrid](/images/documents_subgrid.png "Documents Subgrid")

A good friend of mine [Rob Nightingale](https://www.linkedin.com/in/rob-nightingale-bba8a89/) once told me (ok - I needed telling more than once 🤣) that you should always execute a process manually **before** trying to automate it so that's what I did next. I uploaded an image to the **Documents on Default Site 1** Document Location and found that, within SharePoint, the image had been stored inside a folder that had been named with the following convention: **Name_RowId**: 

![Document Location](/images/doc_location.png "Document Location")