---
title: Workday Quick Start Guide
description: A quick start guide for customer that wants to use Adobe Sign in their Workday environments.
uuid: 10bf8ee8-9075-44d1-a836-e454950e2d9a
products: Adobe Sign
content-type: reference
discoiquuid: 13135c88-4c39-4707-b7ba-63ff94769258
locnotes: All languages; screenshots to follow what's there already (seems there is a mix within a given language version of the article)
type: Documentation
solution: Acrobat Sign
role: User, Developer
topic: Integrations
exl-id: 8b6fa8b4-e240-4ebe-ae2a-8807d75a6c69
---
# [!DNL Workday] Quick Start Guide{#workday-quick-start-guide}

[**Contact Adobe Sign Support**](https://www.adobe.com/go/adobesign-support-center)

## Overview {#overview}

This document is designed to help [!DNL Workday] administrators understand how to customize the [!DNL Workday] Business Processes to include Adobe Sign for obtaining e-signatures. To use Adobe Sign within [!DNL Workday], you must know how to create and modify [!DNL Workday] items such as:

* [!UICONTROL Business Process Framework]
* Tenant Set-up and configuration
* Reporting and [!DNL Workday] Studio Integration

## Accessing Adobe Sign within [!DNL Workday] {#access-adobe-sign}

[!UICONTROL Adobe Sign electronic signature capability] is surfaced as [!UICONTROL Review Document Step] action within the [!UICONTROL Business Process Framework (BPF)] and as a Distribute Documents task.

## [!UICONTROL Review Document Step] {#review-document-step}

Adobe Sign for [!DNL Workday] is exposed via the [!UICONTROL Review Document Step] that you can add to any of over 400 Business Processes within [!DNL Workday], including [!UICONTROL Offer], [!UICONTROL Distribute Documents and Tasks], [!UICONTROL Propose Compensation], and more.

You may refer to the [[!DNL Workday] community articles on [!UICONTROL Review Document Step]](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/TboWWKQemecNipWgxLAjqg).

There is a 1:1 relationship between [!UICONTROL [!UICONTROL Review Document Step]s] and billable transactions with Adobe Sign. You can combine multiple documents within a single [!UICONTROL Review Document Step] and they are presented as a single package for signature. 

**Note**: Only a single *Dynamic* document can be referenced within a specific [!UICONTROL Review Document Step].

To define a functional [!UICONTROL Review Document Step]:

1. Insert a [!UICONTROL Review Document Step].
1. Specify the Groups (roles) that can act upon the [!UICONTROL Review Document Step].

![The Business Process steps](images/insert-review-doc-steptornm-575.png)

To configure the [!UICONTROL Review Document Step]:

1. Specify the *[!UICONTROL eSignature Integration type]* as *[!UICONTROL eSign by Adobe]*.

1. Add rows to the Signature Grid.

    * The signature grid specifies the serial order in which the document is routed for signature. Each row can contain one or more roles and each row represents a step in the signing process.
    * Every member of the role within a particular step is notified that a signing event is pending.
    * Once a single person from the role signs, the row step is completed and the document is moved to the next row step.
    * When all rows have been signed, the [!UICONTROL Review Document Step] is complete.

1. Specify the document to be signed. If the document is an [!UICONTROL Offer BP], you can use it from a Generate Document step. Otherwise, choose an existing document or report.

1. Repeat step 3 for as many documents as you require.

    ![Configure Review Document Step](images/configure-rd-stepsmaller-575.png)

1. Optionally, add a ‘redirect user’ for capturing ‘decline to sign’ actions. When users decline, [!DNL Workday] reroutes the documents to a configured security group for review.

From the related actions menu of a [!UICONTROL Review Document Step], select **[!UICONTROL Business Process]** > **[!UICONTROL Maintain Redirect]**. Next, select one of the following:

* **[!UICONTROL Send Back]**: To enable security group members to send a step back to a prior step in the business process. The business process restarts from that step.
* **[!UICONTROL Move to Next Step]**: To enable security group members to forward a step to the next step in the business process.
* **[!UICONTROL Security Groups]**: To redirect steps in the business process flow. Security groups that display at this prompt are selected in the business process security policy in the Redirect section.

## Business process step notes {#business-process-step-notes}

The [!UICONTROL Business Process Framework] is powerful; however, you must ensure that:

* Every Business Process must have a completion step, which is ideally at the end of the business process.

* A completion step is set off the related actions menu of the search icon. This is possible only while “viewing” the BP and not while “editing” it.

* Every step of the business process is executed sequentially.

    You can change the order of a step by changing the order value. For instance, to insert a step between items “c” and “d”, specify a new item as “ca”.

### Example: offer {#example-offer}

The Offer BP is a sub process of the [!UICONTROL Job Application Dynamic BP] that must be configured to execute the Offer BP. It is triggered when the Job Application state is moved to “[!UICONTROL Offer]” or “[!UICONTROL Make Offer]”.

In the below example, a [!UICONTROL Review Document Step] is using a Dynamic Document step for both North America and Japan.

![Example of a [!DNL Workday] Business Process](images/bp-for-offersmaller-575.png)

This BP does the following:

* Asks the initiator of the BP to propose compensation for the candidate (step b).
* Uses a step condition to test whether the current country is NOT Japan.

    If true, it executes step “ba” which uses an English language document.
    
    If false, it executes step “bb” which uses a Japanese language document.

* Defines the signature process in the [!UICONTROL Review Document Step] “bc”.
* Defines the decision point to make an offer in the required completion step “d”.

The Dynamic document being generated in step “ba” is called [!UICONTROL Offer Letter] and contains a single text block named [!UICONTROL Rapid Offer]. You can add multiple text blocks such as header, salutation, compensation, stock, closing, terms, and more as required.

![[!DNL Workday] view document page](images/offer-letter-575.png)

The Dynamic offer letter below is created in the [!DNL Workday] rich text editor. The items highlighted in *gray* are [!DNL Workday] provided objects that reference contextual data.

Items in {{brackets}} are [Adobe Text tags](https://adobe.com/go/adobesign_text_tag_guide).

![Example dynamic form](images/script.png)

Within the [!UICONTROL Review Document Step], the dynamic document is referenced from the previous step and defines the sequential signature process via two signing groups.

The behavior illustrated below routes the dynamically generated document first to the Hiring Manager, and then to the Candidate.

![[!DNL Workday] signing groups being defined](images/configure-rd-stepsmaller-575.png) 

### Example: Distribute documents {#example-distribute-documents}

Introduced in [!DNL Workday] 30, the Mass Distribute Documents or Tasks task can be used to send a single document to a large group (&lt;20K) of individual signers. It is limited to a single signature per document. Creation of a distribution is performed by accessing the ‘[!UICONTROL Create Distribute Documents or Tasks]’ action from the search bar.

Example: Send an employee equity choice form to all managers with [!UICONTROL Global Modern Services]. You can further filter it to individual managers, if desired.

You can also access the **View Distribute Documents or Tasks** report to track the progress of the distribution.

![](images/create-distributedocumentsortasks.png) 

### Example: Reporting {#example-reporting}

[!DNL Workday] has a rich reporting infrastructure. To look at the details of the Adobe Sign process, inspect the elements of the *Review Document Event*.

Below is a simple custom report that can be run across all BPs looking for Adobe Sign transactions and their status.

![Example of a [!DNL Workday] Custom Report](images/review-document-eventsmaller-575.png)

The following report was generated by looking at Offer, Onboarding, and Propose Compensation BPs within an implementation tenant.

You can see:

* The documents out for signature
* The associated BP step
* The next person awaiting signature

![Example of a [!DNL Workday] Report using three objects](images/workday-reportsmaller-575.png) 

## Signed documents {#signed-documents}

The [!DNL Workday] signature cycle suppresses all email notifications by Adobe Sign. Users are informed of pending actions within their [!DNL Workday] inbox.

Once a document is signed by all Signature Groups, a copy of the signed document is distributed to all the members of the Signature Group via email.

To suppress this behavior, you may contact your [!UICONTROL Adobe Sign Success Manager] or the [Adobe Sign Support team](https://adobe.com/go/adobesign-support-center).

Within [!DNL Workday], you can access the signed documents on the full process record. You may find:

* Worker documents on the Worker Profile, and
* Candidate documents (offer letters) on the Candidate profile.

The below image shows a signed offer letter for the candidate Chris Foxx. 

![Example [!DNL Workday] offer letter](images/offer.png) 

## Support {#support}

### [!DNL Workday] support {#workday-support}

[!DNL Workday] is the integration owner, and should be your first point of contact for questions about the scope of the integration, feature requests, or problems in day to day function of the integration.

The [!DNL Workday] community has several good articles on how to troubleshoot the integration and generate documents:

* [Troubleshoot eSignature Integrations](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/zhA~hYllD3Hv1wu0CvHH_g)
* [Review Documents Step](https://doc.workday.com/#/reader/3DMnG~27o049IYFWETFtTQ/TboWWKQemecNipWgxLAjqg)  
* [Dynamic Document Generation](https://community.workday.com/node/176443)
* [Offer Document Generation Configuration tips](https://community.workday.com/node/183242)

### Adobe Sign support {#adobe-sign-support}

Adobe Sign is the integration partner, and should be contacted if the integration is failing to obtain signatures, or if notification of pending signatures fails.

Adobe Sign Customers should contact their [!UICONTROL Customer Success Manager] for support. Alternatively, [!UICONTROL Adobe Technical Support] can be reached by phone: 1-866-318-4100, wait for product list then enter: 4 and then 2 (as prompted).

* [Adding Adobe Text Tags to Documents](https://www.adobe.com/go/adobesign_text_tag_guide)

<!--
[Download PDF](images/adobe-sign-for-workday-quick-start-guide-2016.pdf)
-->
