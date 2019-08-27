---
title: IActiveScriptSite::OnStateChange |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptSite.OnStateChange
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptSite_OnStateChange
ms.assetid: 3e9c5cbe-ca8e-426a-84fd-04e9c2daac7e
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ad5719a93aec2940f1180a6ff45a028b937b0dfe
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62992539"
---
# <a name="iactivescriptsiteonstatechange"></a>IActiveScriptSite::OnStateChange
通知主机脚本引擎已更改状态。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT OnStateChange(  
    SCRIPTSTATE ssScriptState  // new state of engine  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ssScriptState`  
 [in]值，该值指示新的脚本状态。 请参阅[IActiveScript::GetScriptState](../../winscript/reference/iactivescript-getscriptstate.md)方法有关的状态说明。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)