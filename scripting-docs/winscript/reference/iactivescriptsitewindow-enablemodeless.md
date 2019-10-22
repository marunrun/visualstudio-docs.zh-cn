---
title: IActiveScriptSiteWindow：： EnableModeless |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptSiteWindow.EnableModeless
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptSiteWindow_EnableModeless
ms.assetid: 83fe4f62-8e97-4f03-bc6f-d90aa888657d
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 756bda6209b6209ff14f6d67fef18faaed0b5618
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72574126"
---
# <a name="iactivescriptsitewindowenablemodeless"></a>IActiveScriptSiteWindow::EnableModeless
使宿主启用或禁用其主窗口以及任何无模式对话框。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT EnableModeless(  
    BOOL fEnable  // enable flag  
);  
```  
  
#### <a name="parameters"></a>参数  
 `fEnable`  
 中标志，如果 `TRUE`，将启用主窗口和无模式对话框，如果 `FALSE`，则禁用主窗口和无模式对话框。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`; 如果发生错误，则返回 `E_FAIL`。  
  
## <a name="remarks"></a>备注  
 此方法与 `IOleInPlaceFrame::EnableModeless` 方法相同。  
  
 对此方法的调用可以嵌套。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptSiteWindow](../../winscript/reference/iactivescriptsitewindow.md)