---
Description: 'The Windows Installer provides many built-in actions for performing the installation process. For a list of these actions, see the Standard Actions Reference.'
ms.assetid: 'fc370ab4-93f3-4e1e-9468-3454d4fee0be'
title: Custom Actions
---

# Custom Actions

The Windows Installer provides many built-in actions for performing the installation process. For a list of these actions, see the [Standard Actions Reference](standard-actions-reference.md).

Standard actions are sufficient to execute an installation in most cases. However, there are situations where the developer of an installation package finds it necessary to write a custom action. For example:

-   You want to launch an executable during installation that is installed on the user's machine or that is being installed with the application.
-   You want to call special functions during an installation that are defined in a dynamic-link library (DLL).
-   You want to use functions written in the development languages Microsoft Visual Basic Scripting Edition or Microsoft JScript literal script text during an installation.
-   You want to defer the execution of some actions until the time when the installation script is being executed.
-   You want to add time and progress information to a ProgressBar control and a TimeRemaining Text control.

The following sections describe custom actions and how to incorporate them into an installation package:

-   [About Custom Actions](about-custom-actions.md)
-   [Using Custom Actions](using-custom-actions.md)
-   [Custom Action Reference](custom-action-reference.md)
-   [Summary List of All Custom Action Types](summary-list-of-all-custom-action-types.md)

 

 


