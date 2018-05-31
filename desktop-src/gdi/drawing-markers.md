---
Description: You can use the line functions to draw markers.
ms.assetid: 69114875-f3e0-45e9-8e87-1f4e9de08db1
title: Drawing Markers
ms.date: 05/31/2018
ms.topic: article
ms.author: windowssdkdev
ms.prod: windows
ms.technology: desktop
---

# Drawing Markers

You can use the line functions to draw markers. A marker is a symbol centered over a point. Drawing applications use markers to designate starting points, ending points, and control points. Spreadsheet applications use markers to designate points of interest on a chart or graph.

In the following code sample, the application-defined Marker function creates a marker by using the [**MoveToEx**](/windows/win32/Wingdi/nf-wingdi-movetoex?branch=master) and [**LineTo**](/windows/win32/Wingdi/nf-wingdi-lineto?branch=master) functions. These functions draw two intersecting lines, 20 pixels in length, centered over the cursor coordinates.


```C++
void Marker(LONG x, LONG y, HWND hwnd) 
{ 
    HDC hdc; 
 
    hdc = GetDC(hwnd); 
        MoveToEx(hdc, (int) x - 10, (int) y, (LPPOINT) NULL); 
        LineTo(hdc, (int) x + 10, (int) y); 
        MoveToEx(hdc, (int) x, (int) y - 10, (LPPOINT) NULL); 
        LineTo(hdc, (int) x, (int) y + 10); 

    ReleaseDC(hwnd, hdc); 
} 
```



The system stores the coordinates of the cursor in the *lParam* parameter of the [**WM\_LBUTTONDOWN**](_win32_wm_lbuttondown_cpp) message when the user presses the left mouse button. The following code demonstrates how an application gets these coordinates, determines whether they lie within its client area, and passes them to the Marker function to draw the marker.


```C++
// Line- and arc-drawing variables  
 
static BOOL bCollectPoints; 
static POINT ptMouseDown[32]; 
static int index; 
POINTS ptTmp; 
RECT rc; 
 
    case WM_LBUTTONDOWN: 
 
 
        if (bCollectPoints &amp;&amp; index < 32)
        { 
            // Create the region from the client area.  
 
            GetClientRect(hwnd, &amp;rc); 
            hrgn = CreateRectRgn(rc.left, rc.top, 
                rc.right, rc.bottom); 
 
            ptTmp = MAKEPOINTS((POINTS FAR *) lParam); 
            ptMouseDown[index].x = (LONG) ptTmp.x; 
            ptMouseDown[index].y = (LONG) ptTmp.y; 
 
            // Test for a hit in the client rectangle.  
 
            if (PtInRegion(hrgn, ptMouseDown[index].x, 
                    ptMouseDown[index].y)) 
            { 
                // If a hit occurs, record the mouse coords.  
 
                Marker(ptMouseDown[index].x, ptMouseDown[index].y, 
                    hwnd); 
                index++; 
            } 
        } 
        break; 
```



 

 


