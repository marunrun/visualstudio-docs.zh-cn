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
ms.openlocfilehash: 9200515b2c975fb1fa5b2acda7c261cb684d85b4
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72577346"
---
# <a name="ijsdebugprocess-interface"></a>IJsDebugProcess 接口
提供用于检查和控制目标进程的例程。  
  
## <a name="syntax"></a>语法  
  
```cpp
IJsDebugProcess : public IUnknown;  
```  
  
## <a name="members"></a>Members  
  
### <a name="public-methods"></a>公共方法  
  
|“属性”|描述|  
|----------|-----------------|  
|[IJsDebugProcess::CreateBreakPoint 方法](../../winscript/reference/ijsdebugprocess-createbreakpoint-method.md)|在指定文档位置设置断点。|  
|[IJsDebugProcess::CreateStackWalker 方法](../../winscript/reference/ijsdebugprocess-createstackwalker-method.md)|堆栈查看程序的工厂方法。|  
|[IJsDebugProcess::PerformAsyncBreak 方法](../../winscript/reference/ijsdebugprocess-performasyncbreak-method.md)|将脚本引擎置于中断模式下，使其在下一个脚本指令处中断。|  
  
## <a name="requirements"></a>要求  
 **标头：** jscript9diag  
  
## <a name="see-also"></a>请参阅  
 [Windows 脚本接口参考](../../winscript/reference/windows-script-interfaces-reference.md)