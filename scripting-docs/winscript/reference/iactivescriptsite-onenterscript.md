---
title: IActiveScriptSite::OnEnterScript | Microsoft Docs
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
ms.openlocfilehash: 5505b30bbfd4e1cbc33022d38d7b7170ffd37dd3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62992692"
---
# <a name="iactivescriptsiteonenterscript"></a>IActiveScriptSite::OnEnterScript
通知主机脚本引擎已开始执行的脚本代码。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT OnEnterScript(void);  
```  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。  
  
## <a name="remarks"></a>备注  
 到脚本引擎，脚本引擎必须在每个进入或重入调用此方法。 例如，如果该脚本调用一个对象，然后触发由脚本引擎处理事件，脚本引擎必须调用`IActiveScriptSite::OnEnterScript`之前执行该事件，并必须调用[IActiveScriptSite::OnLeaveScript](../../winscript/reference/iactivescriptsite-onleavescript.md)执行事件之后、 之前返回到触发事件的对象的方法。 可以嵌套调用此方法。 每个调用此方法需要相应地调用`IActiveScriptSite::OnLeaveScript`。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)