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
  - PowerAutomate
---
I recently had a requirement for Field Service Engineers to be able to save multiple photos captured from the camera control in a Canvas App to the SharePoint Document Location associated with the Job record that they are working on - thereby giving the Administrators in the office full visibility of the photos from within the Model-Driven App that they use for scheduling the Jobs.

In order to achieve this I needed to configure:

1. A Model-Driven App; and
2. A Canvas App; and
3. A Power Automate Flow.

## The Model-Driven App

In terms of the Model-Driven app I needed to do two things:

1. Set the default document management settings via [Power Platform admin center](https://admin.powerplatform.microsoft.com/environments) > Your Environment > Settings > Integration > Document management settings:

![Document management settings](/images/dm_settings.png "Document management settings modal")

2. Add a related Documents Subgrid to the Main form of the Jobs table:

![Documents Subgrid](/images/documents_subgrid.png "Documents Subgrid")

A good friend of mine [Rob Nightingale](https://www.linkedin.com/in/rob-nightingale-bba8a89/) once told me (ok - I needed telling more than once 🤣) that you should always execute a process manually **before** trying to automate it so that's what I did next. I uploaded an image to the **Documents on Default Site 1** Document Location and found that, within SharePoint, the image had been stored inside a folder that had been named with the following convention: **Name_RowId**: 

![Document Location](/images/doc_location.png "Document Location")

## The Canvas App

In terms of the Canvas App I started from Microsoft Dataverse data (Jobs table) and added the Job ID column to the Edit Screen so that I'd be able to pass this to my Power Automate flow.

I then created another screen with the following components:

1. Camera
2. Blank Horizontal Gallery
3. Clear Button
4. Submit Button

![Camera Control Screen](/images/camera_control_screen.png "Camera Control Screen")

### Camera control

I added the following code to the **OnSelect** property of the control:

```yaml
Collect(colCameraImages, Self.Photo)
```

### Gallery control

I added the following to the **Items** property of the control 

```yaml
colCameraImages
```

### Clear Button

I added the following code to the **OnSelect** property of the control:

```yaml
Clear(colCameraImages)
```

### Submit Button

This is where it got a bit tricky and interesting. I was perplexed as to how to I could add a unique name to each image and get the whole collection to Power Automate... until I came across this lifesaver of an article by [Mikael Svenson](https://www.techmikael.com/2017/05/saving-collection-of-images-from.html).

As a result of that article I added the following code to the **OnSelect** property of the control:

```yaml
ForAll(
    colCameraImages,
    Collect(
        SubmitData,
        {
            filename: Concatenate(
                Text(
                    Now(),
                    DateTimeFormat.LongDate
                ),
                Mid(
                    "0123456789ABCDEFGHIJKLMNOPQRTSTIUVWXYZ",
                    1 + RoundDown(
                        Rand() * 36,
                        0
                    ),
                    1
                ),
                Mid(
                    "0123456789ABCDEFGHIJKLMNOPQRTSTIUVWXYZ",
                    1 + RoundDown(
                        Rand() * 36,
                        0
                    ),
                    1
                ),
                ".jpg"
            ),
            filebody: Url
        }
    )
);
```

### The Power Automate Flow

I added a **PowerApps** step, followed by a **(Dataverse) Get a row by ID** step:

![Getting a row by ID](/images/getarowbyid.png "Getting a row by ID")

In the **Row ID** column for the **Get a row by ID**, from the Dynamic Content modal, I chose **Ask in PowerApps** which generated **GetarowbyID_RowID** "variable" for me. I would be passing the **Job ID** value from my Canvas App to this "variable" so I returned to the app to test this before building out the rest of the flow:

## The Canvas App: Part 2

I added the following code to the **OnSelect** property of the Submit Button control:

```yaml
SaveToSharePointDocumentLibrary.Run(Set(JobID, Job_DataCard1.Default));
```

I then previewed the app and selected the Submit Button in order to trigger my flow:

![Flow Run](/images/flow_success.png "Flow Run")

The flow run was successful but I noticed something at this point - the **JobID** that had been passed to the flow contained dashes - as is often the case with a GUID. This wasn't a problem in and of itself, but I would be using this **JobID** in the SharePoint file path for my images and I already knew from my manual upload that the **JobID** part of the file path didn't contain any dashes:



![File Path](/images/docs_file_path.png "File Path")