---
title: NM\_TVSTATEIMAGECHANGING notification code
description: Sent by a tree-view control to its parent window that the state image is changing. This notification code is sent in the form of a WM\_NOTIFY message.
ms.assetid: '8e42d8b3-5e76-4d03-94b0-3e4583669095'
keywords: ["NM_TVSTATEIMAGECHANGING notification code Windows Controls"]
topic_type:
- apiref
api_name:
- NM_TVSTATEIMAGECHANGING
api_location:
- Commctrl.h
api_type:
- HeaderDef
---

# NM\_TVSTATEIMAGECHANGING notification code

Sent by a tree-view control to its parent window that the state image is changing. This notification code is sent in the form of a [**WM\_NOTIFY**](wm-notify.md) message.


```C++
NM_TVSTATEIMAGECHANGING
        
    lpnmtsic = (LPNMTVSTATEIMAGECHANGING) lParam;
```



## Parameters

<dl> <dt>

*lParam* 
</dt> <dd>

A pointer to an [**NMTVSTATEIMAGECHANGING**](nmtvstateimagechanging.md) structure that contains additional information about this notification.

</dd> </dl>

## Return value

The return value is ignored by the control.

## Requirements



|                                     |                                                                                       |
|-------------------------------------|---------------------------------------------------------------------------------------|
| Minimum supported client<br/> | Windows�Vista \[desktop apps only\]<br/>                                        |
| Minimum supported server<br/> | Windows Server�2008 \[desktop apps only\]<br/>                                  |
| Header<br/>                   | <dl> <dt>Commctrl.h</dt> </dl> |



�

�




