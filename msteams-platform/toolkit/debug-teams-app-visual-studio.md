---
author: surbhigupta
title: Debug your Teams app for Visual Studio
description: In this module, learn how to debug your Teams app locally in Visual Studio using Teams Toolkit
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/21/2022
---

# Debug your Teams app locally using Visual Studio

Teams Toolkit helps you to debug and preview your Microsoft Teams app locally. Debug is a process of building, checking, detecting, and correcting issues or bugs in your app. Debug ensures that the program runs successfully. Visual Studio allows you to debug tab, bot, message extension. Teams Toolkit supports the following debug features:

* Prepare Teams app dependencies
* Start debugging
* Toggle breakpoints
* Hot reload
* Stop debugging

During the debug process, Teams Toolkit automatically starts app services, initiates debug, and side loads Teams app. After debug, you can preview the Teams app in Teams web client. You can also customize debug settings to use your bot endpoints, or environment variables to load your configured app.

## Prerequisites

| &nbsp; | Install | For using... |
| --- | --- | --- |
| &nbsp; | **Required** | &nbsp; |
| &nbsp; | Visual Studio 2022 version 17.3 | You can install the enterprise edition of Visual Studio, and install the "ASP.NET "workload and Microsoft Teams Development Tools. |
| &nbsp; | Teams Toolkit | A Visual Studio extension that creates a project scaffolding for your app. Use latest version. |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | Microsoft Teams to collaborate with everyone you work with through apps for chat, meetings, call - all in one place. |
| &nbsp; | [Prepare your Microsoft 365 tenant](../concepts/build-and-test/prepare-your-o365-tenant.md) | Access to Teams account with the appropriate permissions to install an app. |
| &nbsp; | [Microsoft 365 developer account](/../concepts/build-and-test/prepare-your-o365-tenant) | Access to Teams account with the appropriate permissions to install an app. |
| &nbsp; | Azure Tools and [Microsoft Azure CLI](/cli/azure/install-azure-cli) | Azure tools to access stored data or to deploy a cloud-based backend for your Teams app in Azure. |
|&nbsp;  | **Optional** | &nbsp; |
|&nbsp; |[Ngrok](https://ngrok.com/) | Ngrok is used to forward external messages from Azure Bot Framework to your local machine.|

## Debug your app locally

You can debug your app locally in Visual Studio using Teams Toolkit by performing:

### Set up ngrok (Only for Bot and Message Extension app)

Use a command prompt to run this command:

```
ngrok http 5130
```

### Set up your Teams Toolkit

Perform the following steps using the Teams Toolkit to debug your app after you create a project:

1. Right-click on your **project**.
1. Select **Teams Toolkit**.
1. Select **Prepare Teams App Dependencies**.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-teamsappdependencies.png" alt-text="Teams app dependencies for local debug":::

   > [!NOTE]
   > In this scenario the project name is MyTeamsApp1

   Your Microsoft 365 account needs to have the side loading permission before you sign in.  Ensure your Teams app can be uploaded to the tenant, otherwise your Teams app can fail to run in Teams Client.

1. Sign in to your **Microsoft 365 Account**.
1. Select **Continue**
   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-signin-m365.png" alt-text="Sign in to Microsoft 365 account":::

   > [!Note]
   > Learn more about sideloading permission by visiting <https://aka.ms/teamsfx-sideloading-option>.

1. Select **Debug**.
1. Select **Start Debugging**, or directly select **F5**.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-Startdebug.png" alt-text="Start Debugging":::

   Visual Studio launches the Teams app inside Microsoft Teams client in your browser.

   > [!Note]
   > Learn more by visiting <https://aka.ms/teamsfx-vs-debug>.

1. After Microsoft Teams is loaded, select **Add** to install your app in Teams.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-add-loadapp.png" alt-text="Select add to load app":::

   > [!TIP]
   > You can also use hot reload function of Visual Studio during debug. Learn more by visiting <https://aka.ms/teamsfx-vs-hotreload>.

   > [!NOTE]
   > Ensure to post HTTP request to '<http://localhost:5130/api/notification>' to trigger notification, when you're debugging Notification Bot app. If you've selected HTTP trigger when creating the project, you can use any API tools such as curl (Windows Command Prompt), Postman, and so on.

   > [!TIP]
   > If you make any changes to Teams app manifest file (/templates/appPackage/manifest.template.json), ensure that you perform the Prepare Teams App Dependencies command. Before you try to run the Teams app again locally.

## Key features of Teams Toolkit

You can see the following key features of Teams Toolkit, that automate the local debugging process of your Teams app:

### Prepare Teams app dependencies

Teams Toolkit prepares local debug dependencies and registers your Teams app in the tenant in your account. For Bot and Message Extension apps, Teams Toolkit will register and configure bot.

### Start debugging

You can perform debugging with a single operation, press **F5** to start debugging. Teams Toolkit builds code, starts services, and the launches app in your browser.

### Toggle breakpoints

You can toggle breakpoints in the source codes of tabs, bots, message extensions, and Azure functions. The breakpoints execute when you interact with the Teams app in your web browser.
The following image shows the toggle breakpoints:

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-toggle-breakpoint.png" alt-text="Local debug toggle breakpoints":::

### Hot reload

Select **Hot Reload** to apply your changes in your Teams app when you want to update and save the source codes simultaneously during debugging.

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-hot-reload.png" alt-text="Select hot reload icon":::

Select the option **Hot Reload on File Save** from the drop-down to enable auto hot reload.

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-hot-reload-filesave.png" alt-text="Select hot reload on file save":::
  
   > [!Tip]
   > To learn more about Hot Reload function of Visual Studio during debug you can visit <https://aka.ms/teamsfx-vs-hotreload>.

### Stop debugging

Select **Stop Debugging** when the local debug is complete.

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-Stopdebug.png" alt-text="Select stop debug icon":::

## Customize debug settings

You can customize debug setting for your Teams app to use your bot endpoints and add environment variables:

### Use your bot endpoint

You can set siteEndpoint configuration in **.fx/configs/config.local.json** to your endpoint.

```
"bot": {
    "siteEndpoint": "https://baidu.com"
}
```

### Add environment variables

You can add **environmentVariables** to **launchSettings.json** file.

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-environment-variables.png" alt-text="Add custom environment variables":::

### Launch Teams app as a web app

You can launch Teams app as a web app instead of running in Teams client.

1. Select **Properties** > **launchSettings.json** in Solution Explorer panel under your project.
1. Remove the **'launchUrl'** from the file.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-launch-teamsapp-webapp.png" alt-text="Launch teams as a web app by removing launchurl":::

1. Right-click on **Solution**.
1. Select **Properties**.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-solution-properties.png" alt-text="Right click solution and select properties":::

1. Select **Configuration Properties** > **Configuration** in the dialogue.
1. Select uncheck the **Deploy** process box.
1. Select **OK**.

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-disable-deploy.png" alt-text="Uncheck deploy in configuration properties ":::

## See also

* [Provision cloud resources using Visual Studio](provision-cloud-resources.md)
* [Deploy Teams app to the cloud using Visual Studio](deploy-teams-app.md)
* [Edit Teams app manifest using Visual Studio](VS-TeamsFx-preview-and-customize-app-manifest.md)
