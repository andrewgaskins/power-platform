---
ROBOTS: NOINDEX,NOFOLLOW
title: "Automate chatbot actions with flows"
description: "Retrieve data and automate processes in your Power Virtual Agents bot with flows."
keywords: "PVA, flow, automate"
ms.date: 01/06/2022

ms.topic: article
author: iaanw
ms.author: iawilt
manager: shellyha
ms.custom: flow, ceX, advanced-authoring
ms.collection: virtual-agent
---

# Add actions to a bot using Power Automate

[!INCLUDE [Build 2022](includes/build-22-disclaimer.md)]

You can help your bot to perform an action by calling a Microsoft Power Automate flow. Flows can help you automate activities or call backend systems. For example, you can use flows with end-user authentication to retrieve information about a user after they've signed in.

Your call flows from within topics as a discrete **Call an action** node. You can utilize flows that have already been created in your Power Apps environment or create a flow from within the Power Virtual Agents [authoring canvas](authoring-create-edit-topics.md).

> [!IMPORTANT]
> To use flows within Power Virtual Agents, they must meet the following requirements:
>
> - A flow can only be called from a topic located in the same [Microsoft Dataverse environment](/powerapps/maker/common-data-service/data-platform-intro) as your bot.
>
> - Flows must also be in a solution in Power Automate. You can [move flows into solutions](#optionally-move-a-flow-from-default-solution-to-another-solution) so they are listed in the authoring canvas.
>
> - [Flow values must be returned synchronously to Power Virtual Agents](#disable-asynchronous-responses-from-flows).

Flows typically use variables to input and output information. The variables can then be used in other nodes within the topic.

## Create a new flow from the Power Virtual Agents authoring canvas

1. Go to the [**Topics page**](authoring-create-edit-topics.md) for the bot you want to edit.

1. Open the authoring canvas for the topic from which you want to call a flow.

1. Select the plus (**+**) button below an existing node to add a new node.

1. In the node selection window, select **Call an action**, and then select **Create a flow**..

    :::image type="content" source="media/advanced-flow/UseCreateFlowOption.jpg" alt-text="Create a new Power Automate flow." border="false":::

Using the **Create a flow** option opens a starter flow template in the [Power Automate portal](https://flow.microsoft.com/) in a separate tab.

:::image type="content" source="media/advanced-flow/PVAConnectorTemplate.JPG" alt-text="Power Automate flow template." border="false":::

> [!NOTE]
> The Power Automate portal automatically opens in the same environment as the bot (using the same user credentials).

This template is an example of a flow that bots can use. To be suitable for bots, a Power Automate flow requires a special **Power Virtual Agents** trigger and response action:

- Flow trigger:  **Power Virtual Agents**  

    :::image type="content" source="media/advanced-flow/PVAConnectorTrigger.JPG" alt-text="Power Virtual Agents trigger." border="false":::

- Response action:  **Power Virtual Agents**  

    :::image type="content" source="media/advanced-flow/PVAConnectorResponse.JPG" alt-text="Power Virtual Agents response." border="false":::

If you make changes to a flow in the Power Automate portal after adding the flow to Power Virtual Agents, you can reload the flow by selecting the **Node menu** (vertical three dots), then **Refresh**.

:::image type="content" source="media/advanced-flow/refresh-flow-node.png" alt-text="Screenshot of flow refresh button." border="false":::

The flow will then be validated again, and any problems detected will need to be fixed before you can save.

## Input and output parameters

Bots can use any number of the following types of inputs and outputs with Power Automate flows:

- Number
- String
- Boolean

The following types aren't supported:

- Object
- Date
- Timestamp
- List [String]
- List [Number]
- List [Boolean]
- List [Object]
- List [Date]
- List [Timestamp]

> [!NOTE]
> A bot can receive up to 1 MB of data from a Power Automate flow in a single action. A bot can pass any amount of data to a Power Automate flow.

### Input parameters

To specify a flow to accept input parameters from a bot, select the **Add an input** option in the **Power Virtual Agents trigger** user interface. Then select the type (string, number, or boolean).

:::image type="content" source="media/advanced-flow/PVAConnector_Inputs_1.JPG" alt-text="Power Virtual Agents trigger input types." border="false":::

For example, you can select **Text** and **Number** to add the following input parameters to the flow:

- **String_Input** of type `string`
- **Number_Input** of type `number`

:::image type="content" source="media/advanced-flow/PVAConnector_Inputs_2.JPG" alt-text="Power Virtual Agents trigger inputs." border="false":::

### Output parameters

To return output parameters to the bot that can be a `string`, `number`, or a `boolean`, select **Add an output** option in **Power Virtual Agents response** user interface, and select the output type.

:::image type="content" source="media/advanced-flow/PVAConnector_Output_1.JPG" alt-text="Power Virtual Agents response output types." border="false":::

For example, you can select **Text** and **Number** to add the following output parameters to the flow and assign return values for them.

- **String_Output** of type `string`
- **Number_Output** of type `number`

:::image type="content" source="media/advanced-flow/PVAConnector_Output_2.JPG" alt-text="Power Virtual Agents response outputs." border="false":::

This example creates a fully functional flow that accepts two parameters, a string and a number, and returns them to a bot as outputs.

Select **Save** to save your new flow.

:::image type="content" source="media/advanced-flow/PVAConnectorTemplate_SAVE.jpg" alt-text="Power Automate flow template - Save." border="false":::

Your flow is saved to the **Default Solution** under the **Solutions** tab on the Power Automate portal.

:::image type="content" source="media/advanced-flow/default-solution.png" alt-text="Power Automate flow template - Default Solution." border="false":::

## Availability of flows

All flows created from the Power Virtual Agents authoring canvas are saved in a **Default Solution** in Power Automate. They can be used by your bots immediately.

In Power Virtual Agents, you can now see this new flow on the list of available actions when you use the **Call an action node** in the authoring canvas.

:::image type="content" source="media/advanced-flow/FlowInActionPicker.png" alt-text="New flow shows up in Action picker." border="false":::

## Optionally move a flow from Default Solution to another solution

To be available to your bots, flows must be stored in a solution in Power Automate. If you don't want to use the **Default Solution** for this purpose, you can move your flows to another solution.

1. On the Power Automate portal, go to the **Solutions** tab to see the available solutions. Use any of the existing solutions or create a new solution for your flows.

1. To create a new solution, select **New solution**.

    :::image type="content" source="media/advanced-flow/NewSolution.jpg" alt-text="Create a solution." border="false":::

1. Give your new solution a name, select **CDS Default Publisher** in the **Publisher** field, enter a **Version** number, and then select **Create**.

    :::image type="content" source="media/advanced-flow/NewSolution_details.jpg" alt-text="Save a new solution." border="false":::

1. On the **Solutions** tab, go to the solution you want to use. Select **Add existing** to add a flow.

    :::image type="content" source="media/advanced-flow/AddExistingFlow.jpg" alt-text="Add existing menu." border="false":::

1. On the **Add existing flow** page, select the **From solutions** tab, and then select your flow. Select **Add** to add your flow to the solution.

    :::image type="content" source="media/advanced-flow/move-flow-from-solution.png" alt-text="Add flow to a solution." border="false":::

   To move a flow from the **My flows** tab to a solution, select the **Outside solutions** option. Select **Add** to add your flow to the solution.

    :::image type="content" source="media/advanced-flow/AddExistingFlow_details.jpg" alt-text="Add flow from outside solutions." border="false":::

## Modify a flow on the Power Automate portal

You can rename and modify your flow on the Power Automate portal. For example, the flow you just created using the template can be updated to provide a weather forecast when called from a bot.

1. In Power Virtual Agents, you can open a flow by using the flow's **View flow details** link on the list of available actions when you use the **Call an action node** in the authoring canvas.

    :::image type="content" source="media/advanced-flow/ModifyFlowInPicker.png" alt-text="Modify a flow from Action Picker." border="false":::

    If you want to update a flow that is already used in your dialog, the same **View flow details** link is available directly in the Action node.

    :::image type="content" source="media/advanced-flow/ModifyFlowInAction.png" alt-text="Modify a flow from Action node." border="false":::

    Using the flow's **View flow details** link launches the Power Automate portal in a separate browser tab, and opens the flow in a **Details** page where you can modify it using the **Edit** command.

    :::image type="content" source="media/advanced-flow/FlowEditDetailsPage.png" alt-text="Edit your flow using the Details page." border="false":::

    To open a flow on the Power Automate portal, go to the **Solutions** tab and open your flow's solution. Use the flow's **Edit menu** to open the flow for editing.

    :::image type="content" source="media/advanced-flow/EditFlow.jpg" alt-text="Open your flow for editing." border="false":::

1. Rename the flow to **Get weather forecast** and then add the following flow input parameters to the **Power Virtual Agents** trigger:

    - City (String)
    - Zipcode (Number)

    :::image type="content" source="media/advanced-flow/RenameFlow.jpg" alt-text="Add inputs to the flow." border="false":::

1. Choose **Add an action** to create a new action below the **Power Virtual Agents** trigger.

    :::image type="content" source="media/advanced-flow/AddAction.jpg" alt-text="Add flow action." border="false":::

1. Enter **MSN weather** into the search box, and then select the **Get forecast for today** action from the list.

    :::image type="content" source="media/advanced-flow/AddMSNWeather.jpg" alt-text="Add Get forecast action." border="false":::

1. A new **MSN Weather Connector** is added to the flow. Under **Location**, select **Add dynamic content**. Select **City** and **Zipcode** from the list.

    :::image type="content" source="media/advanced-flow/AddLocationForMSN.jpg" alt-text="Pass flow's input parameters to MSN Weather connector as location." border="false":::

1. In the response node **Return value(s) to Power Virtual Agents**, add the output parameters that you want to return to the bot. Save your flow.

    - day_summary (String)
    - location (String)
    - chance_of_rain (Number)

    :::image type="content" source="media/advanced-flow/AddDynamicVariables.jpg" alt-text="Add dynamic variables to the flow's response." border="false":::

This flow is now ready to be used in your bots.

## Call a Power Automate flow as an action from a bot

You can call a Power Automate flow from a bot topic using the **Call an action** node. You can then pass variables to the flow and receive flow outputs that can be used in a bot conversation.

These instructions use adding weather information to a flow as an example. If you haven't already, follow the steps under the [Modify a flow on the Power Automate portal](#modify-a-flow-on-the-power-automate-portal) section in this topic to create a weather forecast flow.

**Call a flow from within a topic:**

1. In Power Virtual Agents, go to the [**Topics page**](authoring-create-edit-topics.md) for the bot you want to edit.

1. Create a new topic, and name it **Get weather**.

1. Add the following **trigger phrases**:

    - will it rain
    - today's forecast
    - get weather
    - what's the weather

    :::image type="content" source="media/advanced-flow/create-get-weather-topic.png" alt-text="Create a new Topic." border="false":::

1. By default, a message node is created. Enter **I can help you with that** into the node, and then select the plus (**+**) button under it to add a new node.

    :::image type="content" source="media/advanced-flow/handoff-add-node.png" alt-text="Screenshot of adding a node." border="false":::

1. Add two new **Ask a question** nodes to ask users for the **City (String)** and **Zipcode (Number)** inputs.

    :::image type="content" source="media/advanced-flow/TopicDialogQuestions.jpg" alt-text="Add Topic Dialog questions." border="false":::

1. Select the plus (**+**) button under the question nodes to add a new node. In the node selection window, select **Call an action**, and then select the flow you created earlier called **Get weather forecast**.

    :::image type="content" source="media/advanced-flow/SelectFlowGetWeatherForecast.png" alt-text="Call action." border="false":::

1. Map the flow input blocks to the output variables from the question nodes. **City (text)** gets its value from `Var1 (text)` and **Zipcode (number)** gets its value from `Var2 (number)`.

1. Under the flow's node, add a **Message** node and then enter a message that uses the flow's outputs. For example:

    **Today's forecast for `(x)location`:`{x}day_summary`.
    Chance of rain is `{x}chance_of_rain`%**

    :::image type="content" source="media/advanced-flow/ActionNodeGetWeatherForecast.png" alt-text="Input the variables." border="false":::

1. Select **Save** to save your topic.

## Pass literal values into action input fields

Alternatively, if you'd rather type in a literal value for an action input instead of using a variable as an action input, you can type the value directly into the field.

:::image type="content" source="media/advanced-flow/LiteralActionInput.png" alt-text="Pass literal values into action inputs.":::

## Test your flow and topic

In the **Test chat** pane, start a conversation with the bot by typing in a trigger phrase for the topic that contains the flow.

Enter your city and zip code at the prompt to get today's weather forecast from the bot.

:::image type="content" source="media/advanced-flow/GetWeatherE2E.png" alt-text="Test Dialog." border="false":::

## Disable asynchronous responses from flows

Power Virtual Agents doesn't support Power Automate flows that return values [asynchronously](/power-automate/guide-staff-through-common-tasks-processes#when-to-use-workflows). Creating a new flow within Power Virtual Agents disables this behavior by default.

Flows that have the Asynchronous Response feature enabled may cause an error when your bot tries to run the flow. Instead of running the flow, the bot will say, "Something unexpected happened. We're looking into it. Error code: 3000.".

If you've enabled [Asynchronous Response](/azure/connectors/connectors-native-http#asynchronous-request-response-behavior), you'll need to disable it for the bot to work properly when it runs the flow:

<!-- At the time of writing, steps to find the async response setting (specifically in the PVA step/action) didn't exist in PA docs. If this has changed, please remove these steps and replace with the relevant link. -->
### To disable Asynchronous Response

1. [Locate and modify your flow](#modify-a-flow-on-the-power-automate-portal).

1. In your Power Automate flow, locate the Power Virtual Agents step that returns values.

1. Next to the name of the flow, select the three dots, and then select **Settings**.

    :::image type="content" source="media/advanced-flow/async1.png" alt-text="Open step settings.":::

1. Set **Asynchronous Response** to **Off**, and then select **Done**.

    :::image type="content" source="media/advanced-flow/async2.png" alt-text="Disable asynchronous response.":::

## Troubleshoot your bot

[Test your bot](authoring-test-bot.md) when you make changes to your topics and flows to ensure everything is working as expected. When a bot encounters a problem during a conversation, it will respond with an error message.

You can find most flow-related issues in the [Flow Checker](/power-automate/error-checker), but any issues on the authoring canvas will appear in the [topic checker](authoring-topic-management.md#topic-errors).

[!INCLUDE[footer-include](includes/footer-banner.md)]
