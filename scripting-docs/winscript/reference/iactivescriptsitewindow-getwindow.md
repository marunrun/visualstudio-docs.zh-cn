---
title: IActiveScriptSiteWindow：： GetWindow |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptSiteWindow.GetWindow
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptSiteWindow_GetWindow
ms.assetid: 6284e38c-9dfb-4d69-903d-f243f78c0331
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d8263db447c7692ec7b0982127d63b4bea588a4b
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72574357"
---
# <a name="iactivescriptsitewindowgetwindow"></a>IActiveScriptSiteWindow::GetWindow
检索可充当脚本引擎必须显示的弹出窗口的所有者的窗口的句柄。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetWindow(  
    HWND *phwnd  // address of variable for window handle  
);  
```  
  
#### <a name="parameters"></a>参数  
 `phwnd`  
 弄接收窗口句柄的变量的地址。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`; 如果发生错误，则返回 `E_FAIL`。  
  
## <a name="remarks"></a>备注  
 此方法类似于 `IOleWindow::GetWindow` 方法。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptSiteWindow](../../winscript/reference/iactivescriptsitewindow.md)