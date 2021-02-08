---
layout: layouts/post.njk
title: How To Manually Link Attributes In FetchXML Builder
socialImage: /images/primaryrecordid.png
date: 2021-02-08T08:31:08.872Z
tags:
  - D365
---
I created a Power Apps Portals Web Form that spans across three CDS entities (or Dataverse tables) with the Primary Record Entity being a custom entity named Vacancy Applications. I had to satisfy the following user story:

> As a job seeker, I want the ability to complete an application form(s) over multiple sessions so that I can return to it later if I don’t have the time to complete it in one session.

I needed to create a list of partially completed applications specific to the current portal user. Seems like a job for an Entity List right? Not on this occasion 😒. I'll explain why in a more detailed post.

So with Entity Lists out of the picture I turned to FetchXML and the FetchXML Builder tool for XrmToolBox.

What I found was that I was unable to select the attribute **adx_primaryrecordid** from within the Node Properties of the link-entity **adx_webformsession**. I was able to select **adx_contact** and link to **pfc_applicant**. Seeing as though there can be only one Contact/Applicant per Vacancy Application I thought this would do the trick. Here's the FetchXML:

```xml
`<fetch distinct="true" returntotalrecordcount="true" >
  <entity name="pfc_vacancyapplication" >
    <attribute name="pfc_no" />
    <attribute name="statuscode" />
    <filter>
      <condition attribute="statecode" operator="eq" value="0" />
      <condition attribute="pfc_applicant" operator="not-null" />
      <condition attribute="pfc_vacancy" operator="not-null" />
      <condition attribute="pfc_submissiondeclaration" operator="neq" value="229330000" />
    </filter>
    <link-entity name="pfc_vacancy" from="pfc_vacancyid" to="pfc_vacancy" link-type="inner" alias="vac" >
      <attribute name="pfc_jobtitles" alias="jobtitle" />
      <attribute name="pfc_site" alias="site" />
      <attribute name="pfc_applicationclosedate" alias="closedate" />
      <attribute name="pfc_vacancyid" alias="vacancyid" />
    </link-entity>
    <link-entity name="contact" from="contactid" to="pfc_applicant" alias="app" >
      <filter>
        <condition attribute="accountrolecode" operator="eq" value="2" />
      </filter>
    </link-entity>
    <link-entity name="adx_webformsession" from="adx_contact" to="pfc_applicant" link-type="inner" alias="wfs" >
      <attribute name="adx_webformsessionid" alias="sessionid" />
      <attribute name="adx_currentwebformstep" alias="stepid" />
    </link-entity>
  </entity>
</fetch>`
```

Unfortunately, this did not work and returned multiple records for the same Vacancy Application. I had only two Web Form Sessions:

![Web Form Sessions with only two records displayed](/images/websessions.png "Web Form Sessions Tab Within Web Form on Power Apps Portal")

Yet my query was returning four records:

![FetchXML Builder Screenshot Showing Four Records](/images/partialfetch.png "FetchXML Builder Screenshot Showing Four Records")

I was perplexed to say the least and couldn't get my head around it at all. The usual avenues of Google and Stack Overflow weren't much help either so it was time to phone a friend.

I met [Rob Nightingale](https://www.linkedin.com/in/rob-nightingale-bba8a89/) back in the pre-lockdown days where we actually used to go to real-life CRMUG meetups and have a pint afterwards and I've been a thorn in his side ever since.

Rob's first question was 'Why are you linking on the Contact Entity? ' Typical Rob - straight to the point! I told him why and then he passed on an absolute lifesaver of a tip:

> "Some fields don't seem to exist in FetchXML Builder. If you know they exist then you can use them to create a relationship manually."

What I had to do was type **adx_primaryrecordid** into the *From* column and select **pfc_vacancyapplicationid** from the choices in the *To* column from the Node Properties of the adx_webformsession link-entity and voila:

![FetchXML Builder Screenshot Showing Two Records](/images/primaryrecordid.png "FetchXML Builder Screenshot Showing Two Records")

Cheers Rob!