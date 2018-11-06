---
Description: A callback that notifies the host of instructrion information returned by the associated request.
MS-HAID: vspixengine.IDebugShaderCallback\_ResultInstructions\_DWORD\_BYTE\_arr
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/desktop
title: IDebugShaderCallback::ResultInstructions method
ms.topic: article
ms.date: 05/31/2018
---

# <span id="vspixengine.idebugshadercallback_resultinstructions_dword_byte_arr"></span>IDebugShaderCallback::ResultInstructions method

A callback that notifies the host of instructrion information returned by the associated request.

## Syntax


```C++
);
```

## Parameters

*instructionStreamSize*   
The number of instructions.

*count0\_instructionStream*   
The instructions.

## Return value

If this method succeeds, it returns **S\_OK**. Otherwise, it returns an **HRESULT** error code.

## Requirements

<table><colgroup><col style="width: 50%" /><col style="width: 50%" /></colgroup><tbody><tr class="odd"><td><p>Header</p></td><td>Vspixengine.h</td></tr></tbody></table>

## <span id="see_also"></span>See also

[**IDebugShaderCallback**](https://msdn.microsoft.com/library/windows/desktop/mt422656)

 

 


