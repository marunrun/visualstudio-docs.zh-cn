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
ms.openlocfilehash: bf1b23b191bda29b00bf29f482332301897f9f37
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575669"
---
# <a name="scriptthreadid-constants"></a>SCRIPTTHREADID 常量
用于指定线程的类型。  
  
## <a name="syntax"></a>语法  
  
```cpp
typedef DWORD SCRIPTTHREADID;  
```  
  
## <a name="constants"></a>常量  
  
|常量|值|含义|  
|--------------|-----------|-------------|  
|SCRIPTTHREADID_CURRENT|0xFFFFFFFD|当前正在执行的线程。|  
|SCRIPTTHREADID_BASE|0xFFFFFFFE|基本线程;这就是实例化脚本引擎的线程。|  
|SCRIPTTHREADID_ALL|0xFFFFFFFF|所有线程。|  
  
## <a name="remarks"></a>备注  
 `SCRIPTTHREADID` 类型由 `IActiveScript::GetCurrentScriptThreadID`、`IActiveScript::GetScriptThreadID`、`IActiveScript::GetScriptThreadState`和 `IActiveScript::InterruptScriptThread`使用，但常量只能由 `IActiveScript::GetScriptThreadState` 和 `IActiveScript::InterruptScriptThread`使用。  
  
## <a name="see-also"></a>另请参阅  
 [IActiveScript::GetCurrentScriptThreadID](../../winscript/reference/iactivescript-getcurrentscriptthreadid.md)   
 [IActiveScript::GetScriptThreadID](../../winscript/reference/iactivescript-getscriptthreadid.md)   
 [IActiveScript::GetScriptThreadState](../../winscript/reference/iactivescript-getscriptthreadstate.md)   
 [IActiveScript::InterruptScriptThread](../../winscript/reference/iactivescript-interruptscriptthread.md)