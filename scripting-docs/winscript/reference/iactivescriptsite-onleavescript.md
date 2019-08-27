---
title: IActiveScriptSite::OnLeaveScript |Microsoft Docs
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
ms.openlocfilehash: da39058a8f069c4799835108372d11849d86444e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62992668"
---
# <a name="iactivescriptsiteonleavescript"></a>IActiveScriptSite::OnLeaveScript
通知主机脚本引擎已返回执行脚本代码。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT OnLeaveScript(void);  
```  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。  
  
## <a name="remarks"></a>备注  
 脚本引擎必须在将控制权返还给调用应用程序输入脚本引擎之前调用此方法。 例如，如果该脚本调用一个对象，然后触发由脚本引擎处理事件，脚本引擎必须调用[IActiveScriptSite::OnEnterScript](../../winscript/reference/iactivescriptsite-onenterscript.md)方法，然后再执行该事件时，必须调用`IActiveScriptSite::OnLeaveScript`后返回到触发事件的对象之前执行该事件。 可以嵌套调用此方法。 每次调用`IActiveScriptSite::OnEnterScript`需要相应地调用此方法。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)