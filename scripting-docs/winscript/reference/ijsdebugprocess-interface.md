---
title: IJsDebugProcess 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: a7ad5525-55b7-4c68-a4f7-c508f7877712
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 411679a03daf27046fdcede7ff48e76212bbd2fd
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62557941"
---
# <a name="ijsdebugprocess-interface"></a>IJsDebugProcess 接口
提供用于检查和控制目标进程的例程。  
  
## <a name="syntax"></a>语法  
  
```cpp
IJsDebugProcess : public IUnknown;  
```  
  
## <a name="members"></a>成员  
  
### <a name="public-methods"></a>公共方法  
  
|名称|描述|  
|----------|-----------------|  
|[IJsDebugProcess::CreateBreakPoint 方法](../../winscript/reference/ijsdebugprocess-createbreakpoint-method.md)|将指定的文档位置处设置断点。|  
|[IJsDebugProcess::CreateStackWalker 方法](../../winscript/reference/ijsdebugprocess-createstackwalker-method.md)|堆栈查看器的工厂方法。|  
|[IJsDebugProcess::PerformAsyncBreak 方法](../../winscript/reference/ijsdebugprocess-performasyncbreak-method.md)|将脚本引擎放入中断模式会导致它为在下一个脚本指令发生中断。|  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag.h  
  
## <a name="see-also"></a>请参阅  
 [Windows 脚本接口参考](../../winscript/reference/windows-script-interfaces-reference.md)