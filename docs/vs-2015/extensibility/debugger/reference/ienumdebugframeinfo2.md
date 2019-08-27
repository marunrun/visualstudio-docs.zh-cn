---
title: IEnumDebugFrameInfo2 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEnumDebugFrameInfo2
helpviewer_keywords:
- IEnumDebugFrameInfo2
ms.assetid: 994e30ad-435a-4f9e-9272-d96d9e01099c
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6cc6a0ff332fd6feac72ce4abf38b5319e63c913
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68161015"
---
# <a name="ienumdebugframeinfo2"></a>IEnumDebugFrameInfo2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口枚举[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)结构。  
  
## <a name="syntax"></a>语法  
  
```  
IEnumDebugFrameInfo2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 调试引擎 (DE) 实现此接口可提供用于描述当前调用堆栈的结构列表。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 Visual Studio 调用[EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)若要获取此接口，只要一个断点，异常，halt 中发生或正在调试的程序。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IEnumDebugFrameInfo2`。  
  
|方法|描述|  
|------------|-----------------|  
|[下一页](../../../extensibility/debugger/reference/ienumdebugframeinfo2-next.md)|检索指定的数目的[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)枚举序列中的结构。|  
|[Skip](../../../extensibility/debugger/reference/ienumdebugframeinfo2-skip.md)|跳过指定的数目的[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)枚举序列中的结构。|  
|[Reset](../../../extensibility/debugger/reference/ienumdebugframeinfo2-reset.md)|将枚举序列重置到开头。|  
|[Clone](../../../extensibility/debugger/reference/ienumdebugframeinfo2-clone.md)|创建一个包含当前枚举数形式的相同枚举状态的枚举器。|  
|[GetCount](../../../extensibility/debugger/reference/ienumdebugframeinfo2-getcount.md)|获取数[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)枚举器中的结构。|  
  
## <a name="remarks"></a>备注  
 Visual Studio 将获取此接口来处理断点、 异常或用户生成的暂停正在调试的程序上的第一步。 列表[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)结构表示当前调用堆栈，请使用列表和最早的函数的开始处的当前函数调用调用列表的末尾。 每个`FRAMEINFO`表示堆栈帧，在其中可以计算表达式，并探讨了本地变量的上下文。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)   
 [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)
