---
title: IActiveScript：： GetCurrentScriptThreadID |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScript.GetCurrentScriptThreadID
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScript_GetCurrentScriptThreadID
ms.assetid: b09e8b48-4209-480e-8b71-e99ee9ae2e17
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: dedb16e0c007ed05370fb54835f84f00784c1ae4
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575764"
---
# <a name="iactivescriptgetcurrentscriptthreadid"></a>IActiveScript::GetCurrentScriptThreadID
检索当前正在执行的线程的脚本引擎定义的标识符。 可以在后续调用脚本线程执行控制方法（例如[IActiveScript：： InterruptScriptThread](../../winscript/reference/iactivescript-interruptscriptthread.md)方法）时使用标识符。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetCurrentScriptThreadID(  
    SCRIPTTHREADID *pstidThread  // receives scripting thread identifier  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pstidThread`  
 弄一个变量的地址，该变量接收与当前线程关联的脚本线程标识符。 此标识符的解释留给脚本引擎，但它可以是 Windows 线程标识符的副本。 如果 Win32 线程终止，此标识符将变为未分配，并可随后分配给另一个线程。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`; 如果指定了无效指针，则返回 `E_POINTER`。  
  
## <a name="remarks"></a>备注  
 此方法可从非基线程调用，而不会导致非基本标注宿主对象或[IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)接口。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScript](../../winscript/reference/iactivescript.md)