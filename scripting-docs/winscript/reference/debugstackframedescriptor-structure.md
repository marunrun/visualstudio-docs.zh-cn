---
title: DebugStackFrameDescriptor 结构 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DebugStackFrameDescriptor
apilocation:
- scrobj.dll
helpviewer_keywords:
- DebugStackFrameDescriptor structure
ms.assetid: a86bcb99-41e4-4a26-a1dd-e1458fb73139
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: fddae48178ec6c56ce647f5c4f3a1bff3d81a980
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62955186"
---
# <a name="debugstackframedescriptor-structure"></a>DebugStackFrameDescriptor 结构
枚举堆栈帧并在同一线程上将多个枚举器的输出合并。  
  
## <a name="syntax"></a>语法  
  
```cpp
typedef struct tagDebugStackFrameDescriptor {  
   IDebugStackFrame *pdsf;  
   DWORD_PTR        dwMin;  
   DWORD_PTR        dwLim;  
   BOOL             fFinal;  
   IUnknown         *punkFinal;  
} DebugStackFrameDescriptor;  
```  
  
## <a name="members"></a>成员  
 `pdsf`  
 堆栈帧对象。  
  
 `dwMin`  
 与此堆栈帧相关联的物理地址的最小范围依赖于计算机的表示形式。  
  
 `dwLim`  
 与此堆栈帧关联的物理地址上限依赖于计算机的表示形式。  
  
 `fFinal`  
 指示正在处理帧的标志。  
  
 `punkFinal`  
 如果此参数不是`NULL`，合并当前枚举数应停止，应启动一个新进程。 该对象指示如何启动新的枚举。  
  
## <a name="remarks"></a>备注  
 进程调试管理器使用此结构进行排序的多个脚本引擎的堆栈帧。 按照约定，堆栈便变下。 因此，在体系结构堆栈变大了上的地址应两部分补充。  
  
## <a name="see-also"></a>请参阅  
 [活动脚本调试器常量、枚举和结构](../../winscript/reference/active-script-debugger-constants-enumerations-and-structures.md)