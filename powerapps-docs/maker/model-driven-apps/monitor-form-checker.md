---
title: Monitor and troubleshoot model-driven app form behavior in Power Apps | MicrosoftDocs
description: "Monitor can help you debug and diagnose problems, which help you build faster, more reliable apps."
ms.custom: ""
ms.date: 10/18/2024
ms.reviewer: "matp"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "troubleshooting"
author: "mspilde"
ms.subservice: troubleshoot
ms.author: "mspilde"
tags: 
search.audienceType: 
  - maker
---
# Use Monitor to troubleshoot model-driven app form behavior

Monitor is a tool that can help app makers debug and diagnose problems, which help them build faster, more reliable apps. Monitor provides a deep view into how an app runs by providing a log of all activities in the app as it runs.

Filtering on model-driven app form-related events in Monitor can provide information about related tables, tables, controls, and components on a form in Monitor as your app runs.  

There are many situations where Monitor can help makers understand why a form behaves a certain way. Many form issues are based on business rules, JavaScript, form events, or client API that admins and makers set. Monitor can also help identify whether the issue experienced is designed out-of-the-box or is due to a customization. It provides details that can help answer the following questions:

- [Why aren't rows showing in the related menu of a table?](../../developer/model-driven-apps/troubleshoot-forms.md#related-menu-item-doesnt-appear-in-related-tab)
- [Why a control is disabled/enabled or visible/hidden](../../developer/model-driven-apps/troubleshoot-forms.md#why-a-control-is-disabledenabled-or-visiblehidden)
- Why is a row in a read-only state?

## Filter Monitor for form-related issues

Follow these instructions to understand the behavior of your model-driven app forms.

## Create a Monitor session

Sign in to [Power Apps](https://make.powerapps.com/), select **Apps**, select **...** next to the model-driven app or on the global command bar, and then select **Monitor**.

On the Monitor page, select **Play model-driven** app on the command bar. For more information about creating a Monitor session, go to [Use Monitor to troubleshoot page behavior in model-driven apps](monitor-page-checker.md).

## Filter for forms monitoring

While the app is running in a monitored session, perform actions within the model-driven app consistent with normal use of the app. For example, open and change data using a table form.

1. On the browser window running Monitor, select the **Category** column, and then select **Filter by**.

   > [!div class="mx-imgBorder"]
   > ![Filter on form events in Monitor.](media/monitor-filter-formchecker.png)

1. Select **Equals** or **Contains** from the dropdown list, and then enter *formchecker* in the box. Select **Apply**.

    <img src="media/monitor-formchecker-filter.png" alt="Enter formchecker filter" height="255" width="405"> 

1. The categories are now filtered.  The **Operation** column can be expanded to see the full name of the events that are tracked by selecting and holding the right side of the column and dragging to the right. As you use the app and open and use a form, Monitor updates the list of events.

   > [!div class="mx-imgBorder"] 
   >![Monitored form events displayed.](media/monitor-formchecker-events.png)

## Use Monitor to understand form behavior

For each row with Monitor, detailed information about the form event can be reviewed. For example, imagine you have a question about an error taking place within the form. You go to that form in the app and select the appropriate form component. Then return to the browser with Monitor enabled and review the results either with or without filtering. In this case, there's an error on the composite control. By expanding areas of the **Details**, you can learn more about the event itself.

> [!div class="mx-imgBorder"] 
> ![Monitoring a related menu.](media/monitor-formchecker-related-menu.png)

There are many types of events that are monitored, including the standard form events like `onload`, `onsave`, and `onclose`.

As you continue to use the app that's being monitored, Monitor updates the information in the list of events. For forms, there are many different scenarios that you can troubleshoot and find additional information on the form, control, or table currently being worked on.

## Supported form-checking areas and events

Supported areas for form monitoring include the following.

|App area  |Description  |
|---------|---------|
|Control state   | Details about the state of the visible, enabled, and label source of a control when the form is loaded.     |
|Related menu   | Details about the state of related menu items. Examples:  <br /> Why is a menu item not being displayed? <br /> Where does the menu item come from?     |
|Tab / section / control state change   | Details on who (via the callstack) has caused a form component&mdash;such as a tab, section, or control&mdash;to change the component's visibility and enabled state.        |
|Navigation     | Details about what's causing navigation or unexpected dialogs by tracing the callstack of these `Xrm.Navigation` client API methods: `openAlertDialog(), openConfirmDialog(), openDialog(), openErrorDialog(), navigateTo(), openForm(), openTaskFlow(), openUrl(), openWebResource()`         |
|Unsupported customizations    |  Details about unsupported client API access before the form is ready. Examples: <br /> Accessing `parent.Xrm.Page` in iFrame before the form is fully loaded. <br /> Accessing `Xrm.Page` in a form web resource outside of form handler contexts using `window.setTimeout()` to periodically call the form client API. <br /> Accessing `Xrm.Page` in `updateView()` method of the Power Apps control framework control code.  |

Examples of the supported form-related events in Monitor include:

- FormEvents.onsave
- XrmNavigation
- FormEvents.onload
- FormControls
- TabStateChange.visible
- RelatedMenu
- ControlStateChange.disabled
- ControlStateChange.visible
- SectionStateChange.visible
- UnsupportedClientApi

## Close a monitoring session

To close the monitoring session, close the browser tab where the monitored model-driven app is playing.

## Next steps

For more information about how to troubleshoot issues with forms in a model-driven app, see [Troubleshoot form issues in model-driven apps](../../developer/model-driven-apps/troubleshoot-forms.md).

[Learn about Monitor as a Power Apps tool](../../maker/monitor-overview.md)

[!INCLUDE[footer-include](../../includes/footer-banner.md)]
