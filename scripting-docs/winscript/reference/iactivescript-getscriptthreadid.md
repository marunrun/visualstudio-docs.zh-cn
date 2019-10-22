---
title: IActiveScript：： GetScriptThreadID |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScript.GetScriptThreadID
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScript_GetScriptThreadID
ms.assetid: 2595d76e-30b5-429f-88b4-1d026645dd9b
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 2a0fb1eebfcb6ed100056289fab6bce662f86a7b
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575709"
---
# <a name="iactivescriptgetscriptthreadid"></a>IActiveScript::GetScriptThreadID
检索与给定 Win32 线程关联的线程的脚本引擎定义的标识符。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetScriptThreadID(  
    DWORD dwWin32ThreadID,       // Win32 thread identifier.  
    SCRIPTTHREADID *pstidThread  // Receives scripting thread. identifier  
);  
```  
  
#### <a name="parameters"></a>参数  
 `dwWin32ThreadID` ,  
 中当前进程中正在运行的 Win32 线程的线程标识符。 使用[IActiveScript：： GetCurrentScriptThreadID](../../winscript/reference/iactivescript-getcurrentscriptthreadid.md)函数检索当前正在执行的线程的线程标识符。  
  
 `pstidThread` ,  
 弄一个变量的地址，该变量接收与给定 Win32 线程关联的脚本线程标识符。 此标识符的解释留给脚本引擎，但它可以是 Windows 线程标识符的副本。 请注意，如果 Win32 线程终止，此标识符将变为 "未分配"，并可随后分配给另一个线程。  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|成功。|  
|`E_POINTER`|指定的指针无效。|  
|`E_UNEXPECTED`|不应进行调用（例如，脚本引擎尚未加载或初始化），因此失败。|  
  
## <a name="remarks"></a>备注  
 检索到的标识符可用于对脚本线程执行控制方法（例如[IActiveScript：： InterruptScriptThread](../../winscript/reference/iactivescript-interruptscriptthread.md)方法）进行的后续调用。  
  
 此方法可从非基线程调用，而不会导致非基本标注宿主对象或[IActiveScript：： InterruptScriptThread](../../winscript/reference/iactivescript-interruptscriptthread.md)接口。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScript](../../winscript/reference/iactivescript.md)