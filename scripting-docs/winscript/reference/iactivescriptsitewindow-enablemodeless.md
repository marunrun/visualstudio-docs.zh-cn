---
title: IActiveScriptSiteWindow::EnableModeless |Microsoft Docs
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
ms.openlocfilehash: 4f15135273b98a65903a5d03de87c541fc032cce
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62992921"
---
# <a name="iactivescriptsitewindowenablemodeless"></a>IActiveScriptSiteWindow::EnableModeless
将导致主机启用或禁用其主窗口，以及任何无模式对话框。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT EnableModeless(  
    BOOL fEnable  // enable flag  
);  
```  
  
#### <a name="parameters"></a>参数  
 `fEnable`  
 [in]标记，如果`TRUE`，使主窗口和无模式对话框; 如果`FALSE`，禁用它们。  
  
## <a name="return-value"></a>返回值  
 返回`S_OK`如果成功，或`E_FAIL`是否发生错误。  
  
## <a name="remarks"></a>备注  
 此方法等同于`IOleInPlaceFrame::EnableModeless`方法。  
  
 可以嵌套调用此方法。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptSiteWindow](../../winscript/reference/iactivescriptsitewindow.md)