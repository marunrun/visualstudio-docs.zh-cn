---
title: APPBREAKFLAGS 枚举 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- APPBREAKFLAGS
apilocation:
- scrobj.dll
helpviewer_keywords:
- APPBREAKFLAGS constants
ms.assetid: ea8ed80f-2ddb-4800-bb3b-52b76ba6c7a0
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: de6efbc20843fcaa73965334c18cf0e5c2a0abab
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572659"
---
# <a name="appbreakflags-enumeration"></a>APPBREAKFLAGS 枚举
指示当前的应用程序和线程调试状态。  
  
## <a name="syntax"></a>语法  
  
```cpp  
enum enum_APPBREAKFLAGS{APPBREAKFLAG_DEBUGGER_BLOCK= 0x00000001,APPBREAKFLAG_DEBUGGER_HALT= 0x00000002,APPBREAKFLAG_STEP= 0x00010000,APPBREAKFLAG_NESTED= 0x00020000,APPBREAKFLAG_STEPTYPE_SOURCE= 0x00000000,APPBREAKFLAG_STEPTYPE_BYTECODE= 0x00100000,APPBREAKFLAG_STEPTYPE_MACHINE= 0x00200000,APPBREAKFLAG_STEPTYPE_MASK= 0x00F00000,APPBREAKFLAG_IN_BREAKPOINT= 0x80000000};  
```  
  
## <a name="members"></a>Members  
  
|成员|“值”|描述|  
|------------|-----------|-----------------|  
|APPBREAKFLAG_DEBUGGER_BLOCK|0x00000001|语言引擎应立即在所有线程上通过 BREAKREASON_DEBUGGER_BLOCK 中断。|  
|APPBREAKFLAG_DEBUGGER_HALT|0x00000002|语言引擎应立即与 BREAKREASON_DEBUGGER_HALT 中断。|  
|APPBREAKFLAG_STEP|0x00010000|语言引擎应立即在带有 BREAKREASON_STEP 的单步执行线程中中断。|  
|APPBREAKFLAG_NESTED|0x00020000|应用程序在断点上的嵌套执行中。|  
|APPBREAKFLAG_STEPTYPE_SOURCE|0x00000000|调试器在源级别单步执行。|  
|APPBREAKFLAG_STEPTYPE_BYTECODE|0x00100000|调试器在字节代码级别单步执行。|  
|APPBREAKFLAG_STEPTYPE_MACHINE|0x00200000|调试器正在单步执行计算机级别。|  
|APPBREAKFLAG_STEPTYPE_MASK|0x00F00000|用于分解步骤类型的掩码。|  
|APPBREAKFLAG_IN_BREAKPOINT|0x80000000|断点正在进行。|  
  
## <a name="remarks"></a>备注  
 某些标志指定语言引擎应在下一个机会时中断，而其他标志则指定调试器的单步执行模式。  
  
## <a name="see-also"></a>请参阅  
 [活动脚本调试器常量、枚举和结构](../../winscript/reference/active-script-debugger-constants-enumerations-and-structures.md)   
 [BREAKREASON 枚举](../../winscript/reference/breakreason-enumeration.md)