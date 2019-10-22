---
title: IActiveScriptSite：： OnLeaveScript |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptSite.OnLeaveScript
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptSite_OnLeaveScript
ms.assetid: 79af0e22-fbe3-4fae-8a5f-7af8b857678d
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e9d872948fea14998f9c6f8140467d6e4c83d056
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72570327"
---
# <a name="iactivescriptsiteonleavescript"></a>IActiveScriptSite::OnLeaveScript
向宿主通知脚本引擎已从执行脚本代码返回。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT OnLeaveScript(void);  
```  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。  
  
## <a name="remarks"></a>备注  
 脚本引擎必须先调用此方法，然后才能将控制权返回给进入脚本引擎的调用应用程序。 例如，如果脚本调用了一个对象，该对象随后激发了脚本引擎处理的事件，则脚本引擎必须先调用[IActiveScriptSite：： OnEnterScript](../../winscript/reference/iactivescriptsite-onenterscript.md)方法，然后才能执行该事件，并在执行该事件之后必须调用 `IActiveScriptSite::OnLeaveScript`返回触发事件的对象。 对此方法的调用可以嵌套。 每次调用 `IActiveScriptSite::OnEnterScript` 都需要调用此方法。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)