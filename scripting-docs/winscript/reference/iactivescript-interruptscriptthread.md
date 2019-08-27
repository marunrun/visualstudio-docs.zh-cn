---
title: IActiveScript::InterruptScriptThread | Microsoft Docs
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
ms.openlocfilehash: aa46bc95087b3defaf739cc3473c58e29a93071c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62935503"
---
# <a name="iactivescriptinterruptscriptthread"></a>IActiveScript::InterruptScriptThread
中断正在运行的脚本线程 （事件接收器，立即执行或宏调用） 的执行。 此方法可用于终止卡 （例如，在无限循环） 的脚本。 它可以从非基础线程调用不会导致到主机对象或一个非基本标注[IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)方法。  
  
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
 [in]中断，或以下特殊线程标识符值中的一个线程的标识符：  
  
|“值”|含义|  
|-----------|-------------|  
|SCRIPTTHREADID_ALL|所有线程。 中断应用于当前正在进行的所有脚本方法。 请注意，除非调用方已请求该脚本会断开连接下, 一步的脚本化的事件会导致脚本代码，以便再次运行通过调用[iactivescript:: Setscriptstate](../../winscript/reference/iactivescript-setscriptstate.md) SCRIPTSTATE_DISCONNECTED 方法或设置 SCRIPTSTATE_INITIALIZED 标志。|  
|SCRIPTTHREADID_BASE|基础线程;也就是说，在其中的脚本引擎的线程已实例化。|  
|SCRIPTTHREADID_CURRENT|当前正在执行的线程。|  
  
 `pexcepinfo`  
 [in]地址`EXCEPINFO`结构，其中包含应中止脚本报告的错误信息。  
  
 `dwFlags`  
 [in]与中断相关联的选项标志。 可以是下列值之一：  
  
|“值”|含义|  
|-----------|-------------|  
|SCRIPTINTERRUPT_DEBUG|如果支持，请输入当前脚本执行点处的脚本引擎调试器。|  
|SCRIPTINTERRUPT_RAISEEXCEPTION|如果脚本引擎的语言支持，让脚本能够处理该异常。 否则为脚本方法中止和错误代码返回给调用方;也就是说，事件源或宏调用程序。|  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|成功。|  
|`E_INVALIDARG`|参数无效。|  
|`E_POINTER`|指定了无效的指针。|  
|`E_UNEXPECTED`|不应在调用 （例如，脚本引擎具有尚未加载或初始化）。|  
  
## <a name="see-also"></a>请参阅  
 [IActiveScript](../../winscript/reference/iactivescript.md)