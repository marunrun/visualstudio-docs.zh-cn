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
ms.openlocfilehash: 0862e6fc670be6cd3d3ca9fbf67f453aa0772a90
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63009766"
---
# <a name="appbreakflags-enumeration"></a>APPBREAKFLAGS 枚举
指示当前的应用程序和线程调试状态。  
  
## <a name="syntax"></a>语法  
  
```cpp  
enum enum_APPBREAKFLAGS{APPBREAKFLAG_DEBUGGER_BLOCK= 0x00000001,APPBREAKFLAG_DEBUGGER_HALT= 0x00000002,APPBREAKFLAG_STEP= 0x00010000,APPBREAKFLAG_NESTED= 0x00020000,APPBREAKFLAG_STEPTYPE_SOURCE= 0x00000000,APPBREAKFLAG_STEPTYPE_BYTECODE= 0x00100000,APPBREAKFLAG_STEPTYPE_MACHINE= 0x00200000,APPBREAKFLAG_STEPTYPE_MASK= 0x00F00000,APPBREAKFLAG_IN_BREAKPOINT= 0x80000000};  
```  
  
## <a name="members"></a>成员  
  
|成员|“值”|描述|  
|------------|-----------|-----------------|  
|APPBREAKFLAG_DEBUGGER_BLOCK|0x00000001|语言引擎应与 BREAKREASON_DEBUGGER_BLOCK 立即中断对所有线程。|  
|APPBREAKFLAG_DEBUGGER_HALT|0x00000002|语言引擎应与 BREAKREASON_DEBUGGER_HALT 立即中断。|  
|APPBREAKFLAG_STEP|0x00010000|语言引擎应立即中断 BREAKREASON_STEP 的单步执行线程中。|  
|APPBREAKFLAG_NESTED|0x00020000|在应用程序处于嵌套执行在断点处。|  
|APPBREAKFLAG_STEPTYPE_SOURCE|0x00000000|调试器在源级别单步执行。|  
|APPBREAKFLAG_STEPTYPE_BYTECODE|0x00100000|调试器在字节代码级别单步执行。|  
|APPBREAKFLAG_STEPTYPE_MACHINE|0x00200000|调试器在计算机级别单步执行。|  
|APPBREAKFLAG_STEPTYPE_MASK|0x00F00000|分离出步骤类型的掩码。|  
|APPBREAKFLAG_IN_BREAKPOINT|0x80000000|断点是正在进行中。|  
  
## <a name="remarks"></a>备注  
 某些标志指定语言引擎应在下次有机会，处中断，而其他标志指定调试器单步执行模式。  
  
## <a name="see-also"></a>请参阅  
 [活动脚本调试器常量、 枚举和结构](../../winscript/reference/active-script-debugger-constants-enumerations-and-structures.md)   
 [BREAKREASON 枚举](../../winscript/reference/breakreason-enumeration.md)