---
title: IActiveScriptSite：： OnEnterScript |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptSite.OnEnterScript
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptSite_OnEnterScript
ms.assetid: 1ed9178c-fe80-41c4-b74d-23b85f9cddbf
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 26e4f221014d90478bbbc7bb5771276706c764c0
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72570364"
---
# <a name="iactivescriptsiteonenterscript"></a>IActiveScriptSite::OnEnterScript
向宿主通知脚本引擎已开始执行脚本代码。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT OnEnterScript(void);  
```  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。  
  
## <a name="remarks"></a>备注  
 脚本引擎必须对每个项调用此方法，或在脚本引擎中重入。 例如，如果脚本调用了一个对象，该对象随后激发了脚本引擎处理的事件，则脚本引擎必须在执行该事件前调用 `IActiveScriptSite::OnEnterScript`，并在执行该事件之后必须调用[IActiveScriptSite：： OnLeaveScript](../../winscript/reference/iactivescriptsite-onleavescript.md)方法但在返回到引发事件的对象之前。 对此方法的调用可以嵌套。 对此方法的每个调用都需要对 `IActiveScriptSite::OnLeaveScript` 的相应调用。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)