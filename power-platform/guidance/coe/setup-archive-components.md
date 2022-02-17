---
title: "Set up archive components | MicrosoftDocs"
description: "Learn how to set up the archive components of the CoE Starter Kit"
author: manuelap-msft
manager: devkeydet

ms.component: pa-admin
ms.topic: conceptual
ms.date: 01/24/2022
ms.subservice: guidance
ms.author: mapichle
ms.reviewer: jimholtz
search.audienceType: 
  - admin
search.app: 
  - D365CE
  - PowerApps
  - Powerplatform
---

# Set up archive components

This article will help you to set up the archive components of the governance solution.

>[!NOTE]
>Although the flows are called "archive" flows, they don't automatically archive apps and flows. Instead, they ask makers to back up and archive their apps and flows.

You use this functionality to detect unused objects, and ask makers to either archive or unshare them to keep your tenant tidy.

>[!IMPORTANT]
>This article assumes you have [installed the governance components solution](before-setup-gov.md), and you have your [environment set up](setup.md#create-your-environment) and are signed in with the [correct identity](setup.md#what-identity-should-i-install-the-coe-starter-kit-with).

## Grant makers environment access

If your solution is installed in a production environment, make sure your environment isn't restricted with an [environment security group](limitations.md#security-groups-and-approvals).

If your solution is installed in a Dataverse for Teams environment, you first need to grant access to makers who aren't part of your team in Microsoft Teams so they can participate in approval workflows. [Share an app in a Teams environment](faq.md#share-an-app-from-a-dataverse-for-teams-environment) with your [Power Platform maker group](setup.md#how-will-you-communicate-with-your-admins-makers-and-end-users).

## Configure mandatory environment variables

You'll [update these environment variables](faq.md#update-environment-variables) after you import the solution. Environment variables are used to store application and flow configuration data. This means that you only have to set the value once per environment, and it will be used in all necessary flows and apps in that environment.

>[!TIP]
>Learn how to update environment variables for production and Dataverse for Teams environments: [Update environment variables](faq.md#update-environment-variables).

| Name | Description |
|------|---------------|
| Approval Admin | This is separate from the Admin Email environment variable because you can't use a distribution list for approvals. This environment variable holds the individual or shared account who will be charged with approving the removal of unused orphaned objects. |
| Cleanup Old Objects App URL | (Optional) A link to the Cleanup Old Objects canvas app included in this solution. To make cleanup easier, any communication about old objects that are no longer considered to be useful will include this link. More information: [Get an app URL from a production environment](faq.md#get-a-power-apps-url-from-a-production-environment) or [Get an app URL from a Teams environment](faq.md#add-apps-to-microsoft-teams) |
| Flow Approvals URL | (Optional) A link to the Power Automate approval page for your CoE environment. To make cleanup easier, any communication about old objects that are no longer considered to be useful will include this link. To get the URL, go to flows.microsoft.com for your CoE environment > **Action Items** > **Approvals**. The URL will end in **approvals/received**. |  

## Exempt environments from the archive process

You might want to exempt some environments from the archive process—for example, dedicated environments that are already well-managed. More information: [Establishing an environment strategy](/adoption/environment-strategy)

You can exempt environments from the archive process by using the Power Platform Admin View app.  

### Production environment

If your solution is installed in a production environment, your app will be a model-driven app. Follow these steps:

1. Go to [make.powerapps.com](<https://make.powerapps.com>).
1. Go to your CoE environment.
1. Open the **Power Platform Admin View** app.
1. Select **Environments**, and then select the environment you want to exempt.
1. Set the **Excuse From Archival Flows** field to **Yes**.
1. Select **Save**.

   ![Exclude an environment from the archive process in a production environment.](media/coe-archive2.png "Exclude an environment from the compliance process in a production environment")

### Dataverse for Teams environment

1. Open the Power Apps app in Teams, select **Build**, and then select the team that you've installed the CoE Starter Kit solutions in.
1. Select **Center of Excellence - Core for Teams** > **See All**.
1. Open the **Power Platform Admin View** app.
1. Select **Environments**, and then select the environment you want to exempt.
1. Set the **Excuse From Archival Flows** field to **Yes**.
1. Select **Save**.

   ![Exclude an environment from the archive process in Dataverse for Teams.](media/coe-archive1.png "Exclude an environment from the archive process in Dataverse for Teams")

## Turn on flows

Turn on the following flows, which are installed as part of the governance components solution:

- [Admin | Setup | Ignored Archival Requests](governance-components.md#admin--setup---ignored-archival-requests)
- [Admin | Archive and Clean Up v2 (Check Approval)](governance-components.md#admin--archive-and-clean-up-v2-check-approval)
- [Admin | Archive and Clean Up v2 (Clean Up and Delete)](governance-components.md#admin--archive-and-clean-up-v2-clean-up-and-delete)
- [Admin | Archive and Clean Up v2 (Start Approval for Apps)](governance-components.md#admin--archive-and-clean-up-v2-start-approval-for-apps)
- [Admin | Archive and Clean Up v2 (Start Approval for Flows)](governance-components.md#admin--archive-and-clean-up-v2-start-approval-for-flows)
- [Admin | Email Managers Ignored Approvals](governance-components.md#admin--setup---ignored-archival-requests)

## Share apps with makers

The governance components solution contains the [Archival – Cleanup Unused Objects](governance-components.md#cleanup-old-objects-app) app for makers and admins to manage archive approvals. Share this app with your makers and admins, assigning them the Power Platform Maker SR security role.

More information:

- [Share a canvas app in Power Apps](faq.md#share-an-app-from-a-production-environment)
- [Share a canvas app in Microsoft Teams](faq.md#share-an-app-from-a-dataverse-for-teams-environment)

Consider adding this app to the **Maker - Command Center** for makers to easily find and access it.

## All environment variables

This section includes the full list of environment variables that affect the compliance process, including environment variables with default values. You might have to [update environment variables](faq.md#update-environment-variables) after import.

>[!IMPORTANT]
> You don't have to change the values during setup, just when you need to change the value of an environment variable that you configured during import or when you want to change a default value. To make sure the latest values are picked up, restart all flows after you change environment variables.

Environment variables are used to store application and flow configuration data with data specific to your organization or environment.

| Name | Description | Default value |
|------|---------------|------|
| Approval Admin | This is separate from the Admin Email environment variable because you can't use a distribution list for approvals. This environment variable holds the individual or shared account who will be charged with approving the removal of unused orphaned objects. | None |
| Auto Delete on Archive | Determines whether apps andd flows are deleted when they're approved for deletion in the following flow: Admin \| App Archive and Clean Up - Check Approvals and Archive. The value must be Yes or No.  | Yes |
| Cleanup Old Objects App URL | (Optional) A link to the Cleanup Old Objects canvas app included in this solution. To make cleanup easier, any communication about old objects that are no longer considered to be useful will include this link. More information: [Get an app URL from a production environment](faq.md#get-a-power-apps-url-from-a-production-environment) or [Get an app URL from a Teams environment](faq.md#add-apps-to-microsoft-teams) | None |
| Flow Approvals URL | (Optional) A link to the Power Automate approval page for your CoE environment. To make cleanup easier, any communication about old objects that are no longer considered to be useful will include this link. To get the URL, go to flows.microsoft.com for your CoE environment > **Action Items** > **Approvals**. The URL will end in **approvals/received**.|  None |
| ProductionEnvironment | Set to **No** if you've installed the solution for development or test purposes. This will send approvals to the admin email instead of the maker. | Yes |

## It looks like I found a bug with the CoE Starter Kit; where should I go?

To file a bug against the solution, go to [aka.ms/coe-starter-kit-issues](https://aka.ms/coe-starter-kit-issues).

[!INCLUDE[footer-include](../../includes/footer-banner.md)]