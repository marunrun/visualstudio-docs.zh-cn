---
title: IActiveScript：： InterruptScriptThread |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScript.InterruptScriptThread
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScript_InterruptScriptThread
ms.assetid: 2304d035-6d39-4811-acd3-8a9640fdbef6
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a436f973df05b945c0939f3a593640f567774277
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72577267"
---
# <a name="iactivescriptinterruptscriptthread"></a>IActiveScript::InterruptScriptThread
中断正在运行的脚本线程（事件接收器、立即执行或宏调用）的执行。 此方法可用于终止停滞的脚本（例如，在无限循环中）。 它可以从非基线程调用，而不会导致非基本标注宿主对象或[IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)方法。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT InterruptScriptThread(  
    SCRIPTTHREADID   stidThread,  // identifier of thread  
    const EXCEPINFO *pexcepinfo,  // receives error information  
    DWORD dwFlags  
);  
```  
  
#### <a name="parameters"></a>参数  
 `stidThread`  
 中要中断的线程的标识符，或下列特殊线程标识符值之一：  
  
|“值”|含义|  
|-----------|-------------|  
|SCRIPTTHREADID_ALL|所有线程。 中断应用于当前正在进行的所有脚本方法。 请注意，除非调用方已请求使脚本断开连接，否则，下一个脚本事件会使脚本代码再次运行，方法是使用 SCRIPTSTATE_DISCONNECTED 或 SCRIPTSTATE_INITIALIZED 标志调用[IActiveScript：： SetScriptState](../../winscript/reference/iactivescript-setscriptstate.md)方法字符集.|  
|SCRIPTTHREADID_BASE|基本线程;这就是实例化脚本引擎的线程。|  
|SCRIPTTHREADID_CURRENT|当前正在执行的线程。|  
  
 `pexcepinfo`  
 中@No__t_0 结构的地址，该结构包含应向中止的脚本报告的错误信息。  
  
 `dwFlags`  
 中与中断关联的选项标志。 可以是下列值之一：  
  
|“值”|含义|  
|-----------|-------------|  
|SCRIPTINTERRUPT_DEBUG|如果支持，请在当前脚本执行点输入脚本引擎的调试器。|  
|SCRIPTINTERRUPT_RAISEEXCEPTION|如果脚本引擎的语言支持，让脚本处理异常。 否则，将中止脚本方法，并向调用方返回错误代码;即事件源或宏调用程序。|  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|成功。|  
|`E_INVALIDARG`|参数无效。|  
|`E_POINTER`|指定的指针无效。|  
|`E_UNEXPECTED`|不应进行调用（例如，尚未加载或初始化脚本引擎）。|  
  
## <a name="see-also"></a>请参阅  
 [IActiveScript](../../winscript/reference/iactivescript.md)