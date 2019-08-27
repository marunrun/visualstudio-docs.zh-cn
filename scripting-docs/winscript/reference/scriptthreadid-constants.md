---
title: SCRIPTTHREADID 常量 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- SCRIPTTHREADID
apilocation:
- scrobj.dll
helpviewer_keywords:
- SCRIPTTHREADID
ms.assetid: 1df9940c-ad0c-42d8-96b9-6a6abe2382e6
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: dfbb39d10d552141a68d40a7be3f1715a80f8f57
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62840195"
---
# <a name="scriptthreadid-constants"></a>SCRIPTTHREADID 常量
用于指定线程的类型。  
  
## <a name="syntax"></a>语法  
  
```cpp
typedef DWORD SCRIPTTHREADID;  
```  
  
## <a name="constants"></a>常量  
  
|返回的常量|“值”|含义|  
|--------------|-----------|-------------|  
|SCRIPTTHREADID_CURRENT|0xFFFFFFFD|当前正在执行的线程。|  
|SCRIPTTHREADID_BASE|0xFFFFFFFE|基础线程;也就是说，在其中的脚本引擎的线程已实例化。|  
|SCRIPTTHREADID_ALL|0xFFFFFFFF|所有线程。|  
  
## <a name="remarks"></a>备注  
 `SCRIPTTHREADID`类型由`IActiveScript::GetCurrentScriptThreadID`， `IActiveScript::GetScriptThreadID`， `IActiveScript::GetScriptThreadState`，并`IActiveScript::InterruptScriptThread`，但的仅可使用常量`IActiveScript::GetScriptThreadState`和`IActiveScript::InterruptScriptThread`。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScript::GetCurrentScriptThreadID](../../winscript/reference/iactivescript-getcurrentscriptthreadid.md)   
 [IActiveScript::GetScriptThreadID](../../winscript/reference/iactivescript-getscriptthreadid.md)   
 [IActiveScript::GetScriptThreadState](../../winscript/reference/iactivescript-getscriptthreadstate.md)   
 [IActiveScript::InterruptScriptThread](../../winscript/reference/iactivescript-interruptscriptthread.md)