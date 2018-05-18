---
title: HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Classes
description: The subkeys and registry values associated with the HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Classes key contain information about an application that is needed to support COM functionality.
ms.assetid: 'a5b271d6-f445-45df-a8e4-f6e0194ac824'
---

# HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Classes

The subkeys and registry values associated with the **HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Classes** key contain information about an application that is needed to support COM functionality. This information includes such topics as supported data formats, compatibility information, programmatic identifiers, DCOM, and controls.



| Subkey                                                                         | Description                                                                                                       |
|--------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| [**AppID**](appid-key.md)                                                     | Configuration options for COM-based applications.                                                                 |
| [**CLSID**](clsid-key-hklm.md)                                                | Configuration options for COM classes.                                                                            |
| [**&lt;file\_extension&gt;**](-file-extension--key.md)                        | Associates a file name extension with a ProgID.                                                                   |
| [**FileType**](filetype-key.md)                                               | Used by [**GetClassFile**](getclassfile.md) to match patterns against various file bytes in a non-compound file. |
| [**Interface**](interface-key.md)                                             | Associates an interface name with an interface ID (IID).                                                          |
| [**&lt;ProgID&gt;**](-progid--key.md)                                         | Identifies a class. Note that the ProgID is not guaranteed to be globally unique, unlike a CLSID.                 |
| [**&lt;version-independent ProgID&gt;**](-version-independent-progid--key.md) | Used to determine the latest version of an object application.                                                    |



 

 

 



