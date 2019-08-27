---
title: IActiveScript::GetCurrentScriptThreadID | Microsoft Docs
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
ms.openlocfilehash: 9e1b6e7bae7d78c18e11cd1aac8d0844fb9e90a5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62935651"
---
# <a name="iactivescriptgetcurrentscriptthreadid"></a>IActiveScript::GetCurrentScriptThreadID
检索当前正在执行的线程的脚本引擎定义标识符。 标识符可以如对脚本线程执行控制方法的后续调用中使用[iactivescript:: Interruptscriptthread](../../winscript/reference/iactivescript-interruptscriptthread.md)方法。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetCurrentScriptThreadID(  
    SCRIPTTHREADID *pstidThread  // receives scripting thread identifier  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pstidThread`  
 [out]一个变量来接收与当前线程关联的脚本线程标识符的地址。 此标识符的解释为从左到脚本引擎，但它可以只是一份 Windows 线程标识符。 如果 Win32 线程终止，此标识符将成为未分配，并且随后可分配给另一个线程。  
  
## <a name="return-value"></a>返回值  
 返回`S_OK`如果成功，或`E_POINTER`如果指定了无效的指针。  
  
## <a name="remarks"></a>备注  
 此方法可以从非基础线程调用不会导致到主机对象或一个非基本标注[IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)接口。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScript](../../winscript/reference/iactivescript.md)