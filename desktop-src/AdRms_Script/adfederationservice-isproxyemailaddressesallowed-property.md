---
Description: Specifies or retrieves a Boolean value that indicates whether proxy email addresses can be used to identify users.
audience: developer
author: REDMOND\\markl
manager: REDMOND\\mbaldwin
ms.assetid: c9ef622e-69e1-4c3d-94c6-9c75d874f979
ms.prod: windows-server-dev
ms.technology: active-directory-rights-management
ms.tgt_platform: multiple
title: ADFederationService.IsProxyEmailAddressesAllowed property
ms.date: 05/31/2018
ms.topic: article
ms.author: windowssdkdev
---

# ADFederationService.IsProxyEmailAddressesAllowed property

The **IsProxyEmailAddressesAllowed** property specifies or retrieves a Boolean value that indicates whether proxy email addresses can be used to identify users.

## Syntax


```VB
ADFederationService.IsProxyEmailAddressesAllowed
```



## Property value

This property specifies or retrieves a Boolean value. A value of **True** indicates that proxy email addresses are allowed.

## Remarks

An email account can have more than one identity if it can be accessed in more than one way. Internet access (as opposed to local network access within an organization) is often routed through a proxy server. Specifying **True** for the **IsProxyEmailAddressesAllowed** property allows the AD RMS service to accept alternate address configurations for the same email account.

If the [**IsSupported**](adfederationservice-issupported-property.md) property value is **false**, the **IsProxyEmailAddressesAllowed** property throws an exception.

The ADFS service must be enabled before this property is called. For more information, see [**Enabled**](adfederationservice-enabled-property.md).

## Examples


```VB
DIM config_manager
DIM admin_role

' *******************************************************************
' Create and initialize a ConfigurationManager object.

SUB InitObject()

  CALL WScript.Echo( "Create ConfigurationManager object...")
  SET config_manager = CreateObject _
    ("Microsoft.RightsManagementServices.Admin.ConfigurationManager")      
  CheckError()
    
  CALL WScript.Echo( "Initialize...")
  admin_role=config_manager.Initialize(false,"localhost",80,"","","")
  CheckError()

END SUB

' *******************************************************************
' Specify ADFS information.

SUB SetADFS()
    
  DIM objADFS

  SET objADFS = _
    config_manager.Enterprise.TrustPolicy.ADFederationService
  CheckError()
        
  IF objADFS.IsSupported = TRUE THEN
    objADFS.Enabled = true
    CheckError()

    objADFS.ValidityPeriodInDays = 10
    CheckError()

    objADFS.RightsAccountCertificateRequestUrl = _
        "https://www.example.com"
    CheckError()

    objADFS.IsProxyEmailAddressesAllowed = TRUE
    CheckError()
  END IF

END SUB

' *******************************************************************
' Error checking function.

FUNCTION CheckError()
  CheckError = Err.number
  IF Err.number <> 0 THEN
    CALL WScript.Echo( vbTab & "*****Error Number: " _
                       & Err.number _
                       & " Desc:" _
                       & Err.Description _
                       & "*****")
    WScript.StdErr.Write(Err.Description)
    WScript.Quit( Err.number )
  END IF
END FUNCTION

' *******************************************************************
' Generate a runtime error.

SUB RaiseError(errId, desc)
  CALL Err.Raise( errId, "", desc )
  CheckError()
END SUB
```



## Requirements



|                                     |                                                                                                                         |
|-------------------------------------|-------------------------------------------------------------------------------------------------------------------------|
| Minimum supported client<br/> | None supported<br/>                                                                                               |
| Minimum supported server<br/> | Windows Server 2008<br/>                                                                                          |
| Assembly<br/>                 | <dl> <dt>Microsoft.RightsManagementServices.Admin.dll</dt> </dl> |



## See also

<dl> <dt>

[**ADFederationService**](adfederationservice-object.md)
</dt> </dl>

 

 



