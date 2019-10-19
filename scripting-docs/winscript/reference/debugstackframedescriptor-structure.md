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
ms.openlocfilehash: 910e08ec6d9982354eb71b50d5e916917808f140
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576555"
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
  
## <a name="members"></a>Members  
 `pdsf`  
 堆栈帧对象。  
  
 `dwMin`  
 与此堆栈帧关联的物理地址的较低范围的依赖于计算机的表示形式。  
  
 `dwLim`  
 与此堆栈帧关联的物理地址的上部范围的依赖于计算机的表示形式。  
  
 `fFinal`  
 指示正在处理帧的标志。  
  
 `punkFinal`  
 如果未 `NULL` 此参数，则当前的枚举器合并应停止，并启动新的。 对象指示如何启动新枚举。  
  
## <a name="remarks"></a>备注  
 进程调试管理器使用此结构对多个脚本引擎的堆栈帧进行排序。 按照约定，堆栈会增长。 因此，在堆栈上增长的体系结构中，地址应为2补码。  
  
## <a name="see-also"></a>请参阅  
 [活动脚本调试器常量、枚举和结构](../../winscript/reference/active-script-debugger-constants-enumerations-and-structures.md)