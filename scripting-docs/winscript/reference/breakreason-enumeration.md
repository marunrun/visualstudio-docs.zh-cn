---
title: BREAKREASON 枚举 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- BREAKREASON
apilocation:
- scrobj.dll
helpviewer_keywords:
- BREAKREASON enumeration
ms.assetid: bde07ede-2f9b-4fa2-affc-f9405683f5f7
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 6f656bdf4e3bc85a014ff8d3011708799aa44bcd
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572619"
---
# <a name="breakreason-enumeration"></a>BREAKREASON 枚举
指示造成中断的原因。  
  
## <a name="syntax"></a>语法  
  
```cpp
typedef enum tagBREAKREASON {  
   BREAKREASON_STEP,  
   BREAKREASON_BREAKPOINT,  
   BREAKREASON_DEBUGGER_BLOCK,  
   BREAKREASON_HOST_INITIATED,  
   BREAKREASON_LANGUAGE_INITIATED,  
   BREAKREASON_DEBUGGER_HALT,  
   BREAKREASON_ERROR,  
   BREAKREASON_JIT  
} BREAKREASON;  
```  
  
## <a name="members"></a>Members  
  
|成员|描述|  
|------------|-----------------|  
|BREAKREASON_STEP|语言引擎处于单步执行模式。|  
|BREAKREASON_BREAKPOINT|语言引擎遇到显式断点。|  
|BREAKREASON_DEBUGGER_BLOCK|语言引擎在另一个线程上遇到了调试程序块。|  
|BREAKREASON_HOST_INITIATED|宿主请求中断。|  
|BREAKREASON_LANGUAGE_INITIATED|语言引擎请求了一个分行符。|  
|BREAKREASON_DEBUGGER_HALT|调试器 IDE 请求中断。|  
|BREAKREASON_ERROR|执行错误导致了中断。|  
|BREAKREASON_JIT|由 JIT 调试启动引起的。|  
  
## <a name="see-also"></a>请参阅  
 [活动脚本调试器常量、枚举和结构](../../winscript/reference/active-script-debugger-constants-enumerations-and-structures.md)