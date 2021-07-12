---
title: Workday Installation Guide
seo-title: Adobe Sign for Workday Installation Guide
description: Installation guide for enabling the Adobe Sign integration with Workday
seo-description: Installation guide for enabling the Adobe Sign integration with Workday
uuid: 56478222-fe66-4fa5-aac3-0ecdf2863197
products: SG_ESIGNSERVICES
topic-tags: EchoSign/Integrations
content-type: reference
discoiquuid: 29d55a25-6e2f-4c59-ae7c-c21bb82cecba
locnotes: All languages; screenshots for Tier 1 and 2 only (see the currently published localized page for guidance) 
---

# Workday Installation Guide{#workday-installation-guide}

[**Contact Adobe Sign Support**](https://echosign.zendesk.com/hc/en-us/requests/new?ticket_form_id=34323)

## Overview {#overview}

BEST

This document explains how to integrate Adobe Sign into your Workday tenant. To use Adobe Sign within Workday, you need to know how to create and modify Workday items such as:

* Business Process Framework
* Tenant Set-up and configuration
* Reporting and Workday Studio Integration

The high-level steps to complete integration are: 

* Activate your Administrative account in Adobe Sign (New Customers Only)
* Configure a Group in Adobe Sign to hold the Workday integration user
* Establish the OAuth relationship between Workday and Adobe Sign

## Activate Your Adobe Sign Account {#activating-your-adobe-sign-account}

Existing customers with established accounts can skip to the [Configure Adobe Sign for Workday](#config) step

For customers who are new to Adobe Sign and do not have a pre-existing log-in, an Adobe on-boarding specialist provisions your account (in Adobe Sign) for Workday. Once complete, you receive a confirmation email:

![Image of the Welcome Email from Adobe Sign](images/welcome-email-2020.png)

You need to follow the directions in the email to initialize your account and access your Adobe Sign *Home* page.

![The Adobe Sign Dashboard page](images/classic-home-1.png) 

## Configure Adobe Sign for Workday {#config}

To configure Adobe Sign for Workday, you need to generate following two dedicated objects in the Adobe Sign system:

* **A Workday group**: Workday requires a dedicated “group” within the Adobe Sign account to enable integration functionality. The Adobe Sign group is used to control only the Workday usage of Adobe Sign. Any other potential usage, such as Salesforce.com or Arriba is not impacted. The email notifications are suppressed in Workday group so that the Workday users only receive notifications within their Workday inbox.

* **An authenticating user to hold the integration key**: A Workday group must have only one group level administrator, who is the authoritative holder of the integration key. We recommend that the administrator use a functional email address such as **HR@MyDomain.com** instead of a personal email to reduce the risk of having the user disabled in future and consequently disabling the integration.

### Create a User and Group in Adobe Sign {#create-a-user-and-group-in-adobe-sign}

To create a user in Adobe Sign:

1. Log in to Adobe Sign as the account administrator
1. Navigate to **Account > Users**
1. Click the **circled plus sign** to create a new user 

    ![Image of the navigation path to create a new user](images/navigate-to-group-unbranded.png)

1. In the dialog that opens, provide the new user details:

    * Provide a functional email that you can access.
    * Enter an appropriate First and Last name value.
    * Select **Create a new group for this user** from the User Group.    
    * Provide the *New Group Name* with an intuitive name like “Workday”

    ![The Create a User panel](images/create-user.png)

1. Click **Save**

    It brings you back to the *Users* page that lists the new user with a **CREATED** status. 

    ![A view of the new Created user](images/post-user-creation.png)

To verify the email address of the user with “Created” status:

1. Log in to the new user’s email.
2. Find the “Welcome to Adobe Sign” email.
3. Click where it says **Click here to set your password**.
4. Set the password.

Once you verify the email address, the status of the user changes from "CREATED" to "ACTIVE".

![Image of the new Activated user](images/actived-users-575.png) 

### Define the Authenticating User {#define-the-authenticating-user}

To promote the new user in the Workday group:

1. Navigate to the *Users* page (if not already there).
2. Double-click the user in the Workday group.

    This opens an *Edit* page for the user permissions.

3. Check the **User is a group administrator box**.
4. Click **Save**.

![](images/user-permissions-edit1-575.png) 

## Configure the Workday Tenant {#configure-workday}

To complete the connection between the Workday tenant and Adobe Sign, we need to establish a trusted relationship between the services. Once done, we can add a Review Document step that enables the signature process through Adobe Sign.

**Note**: Adobe Sign is branded as Adobe Document Cloud throughout the Workday environment.

To establish the trusted relationship:

1. Log in to Workday as an account administrator
1. Search for Edit Tenant Setup - Business Processes

    It loads the *Edit Tenant Setup - Business Processes* page

1. Locate the eSignature Configuration section:

    ![](images/esignature_configurations.png)

1. Click **Authenticate with Adobe**.

    This starts the OAuth2.0 authentication sequence.

1. When asked, provide the credentials for the Adobe Sign Group admin that you created earlier.
1. Approve the access to Adobe Sign.

**Note**: Make sure that you completely log out of any other Adobe Sign instance before proceeding.

Once connected, the Adobe configuration enabled checkbox is set and you can begin using Adobe Sign with Workday.

### Configure the Review Document step {#configure-review}

The document for the Review Document step can be either one of the following:

* A static document
* A document generated by a Generate Document step within the same business process
* A formatted report created with the Workday Report Designer

You may add any of these docs with [Adobe Text Tags](https://helpx.adobe.com/sign/using/text-tag.html) to control the look and position of the Adobe Signing specific components. The document source must be specified within the business process definition. It is not possible to upload an ad-hoc document while the business process is executing.

Unique to using Adobe Sign with a Review Document step is the ability to have serialized Signer Groups. This allows you to specify role-based groups that sign in sequence. Adobe Sign does not support parallel signing groups.

For assistance configuring the Review Document step, refer to the [Quick Start guide](https://helpx.adobe.com/sign/using/workday-integration-quick-start-guide.html).  

## Support {#support}

### Workday Support {#workday-support}

Workday is the integration owner, and should be your first point of contact for questions about the scope of the integration, feature requests, or problems in day to day function of the integration.

You may refer to the following Workday community articles on how to troubleshoot the integration and generate documents:

* [Troubleshoot eSignature Integrations](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/zhA~hYllD3Hv1wu0CvHH_g)

* [Review Documents Step](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/TboWWKQemecNipWgxLAjqg)

* [Dynamic Document Generation](https://community.workday.com/saml/login?destination=/articles/176443)

* [Offer Document Generation Configuration tips]()

### Adobe Sign Support {#adobe-sign-support}

Adobe Sign is the integration partner, and should be contacted if the integration is failing to obtain signatures, or if notification of pending signatures fails.

Adobe Sign Customers should contact their Customer Success Manager (CSM) for support. Alternatively, Adobe Technical Support can be reached by phone: 1-866-318-4100, wait for product list then enter: 4 and then 2 (as prompted).

* [Adding Adobe Text Tags to Documents](https://helpx.adobhttps://community.workday.com/node/183242e.com/sign/using/text-tag.html)  

* [Review Document configuration and examples](https://helpx.adobe.com/sign/using/workday-integration-quick-start-guide.html)

## Common Questions {#faq}

### Why is the status not being updated within Workday even the document is fully signed? {#why-is-the-status-not-being-updated-within-workday-even-the-document-is-fully-signed}

The root of this problem can be that the Candidate has not clicked the Submit button in Workday after signing in Adobe Sign.

Per Workday task Check eSignature Signing Status: "To start the process, the user can submit the associated Inbox task."

Per Workday Development: The original signing completes the process only if the user submits the Inbox task after signing the document. The signers have to always submit the Inbox task in Workday after they complete the signing on Adobe Sign. Post signing, the iframe is closed and the user is redirected to the same task where they can click the submit button to complete the process.