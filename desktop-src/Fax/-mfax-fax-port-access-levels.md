---
Description: 'The Fax Service Client API allows your application to query and modify fax port configuration data.'
ms.assetid: 'bd1d8a10-0867-4701-b6ef-d2f2f9f6923c'
title: Fax Port Access Levels
---

# Fax Port Access Levels

The Fax Service Client API allows your application to query and modify fax port configuration data.

## In the Win32 Environment

To allow users access to a port's configuration data, a fax client application must specify the correct fax port access level when it calls the [**FaxOpenPort**](-mfax-faxopenport.md) function. **FaxOpenPort** returns a fax port handle and opens the port according to the specified access level. The application can request one of the following values, depending on the requirements and permissions of the user.



| Value              | Meaning                                                                                                                                                                                                                                            |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| PORT\_OPEN\_QUERY  | Port access level required to query fax port information with calls to the [**FaxGetPort**](-mfax-faxgetport.md), [**FaxEnumPorts**](-mfax-faxenumports.md) and [**FaxGetDeviceStatus**](-mfax-faxgetdevicestatus.md) functions.                |
| PORT\_OPEN\_MODIFY | Port access level required to modify the configuration of a fax port with a call to the [**FaxSetPort**](-mfax-faxsetport.md) function. This access level implicitly grants the access rights associated with the PORT\_OPEN\_QUERY access level. |



 

In addition to requiring that a port be opened with the appropriate access level, the fax service also requires that users have appropriate access rights when querying and modifying port data. To obtain a fax port handle and to query port data, a user must have FAX\_PORT\_QUERY permission. To modify port data, a user must have FAX\_PORT\_SET permission. For more information, see [Fax Client User Access Rights](-mfax-fax-client-user-access-rights.md) and [Fax Device Management](-mfax-fax-device-management.md).

To query a user's access rights, a fax client application can call the [**FaxAccessCheck**](-mfax-faxaccesscheck.md) function. You can use the fax service administration application, a Microsoft Management Console (MMC) snap-in component, to modify port access privileges for users.

## In the COM Implementation Environment

Before your application calls a method that modifies a [FaxPort](-mfax-faxport.md) property, you can call the [**IFaxPort::get\_CanModify**](-mfax-ifaxport-mfax-ifaxport-get-canmodify-cpp.md) method (retrieve the **CanModify** property of the FaxPort object in Microsoft Visual Basic) to ensure that the client has access to modify the port's configuration. For more information, see [Fax Device Management](-mfax-fax-device-management.md).

 

 


