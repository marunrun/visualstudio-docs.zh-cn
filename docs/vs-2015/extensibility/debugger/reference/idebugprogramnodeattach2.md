---
title: IDebugProgramNodeAttach2 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgramNodeAttach2
helpviewer_keywords:
- IDebugProgramNodeAttach2 interface
ms.assetid: 46b37ac9-a026-4ad3-997b-f19e2f8deb73
caps.latest.revision: 4
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 580d4d2432a957bae8c590b3590a11b1a0b5e84e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68148527"
---
# <a name="idebugprogramnodeattach2"></a>IDebugProgramNodeAttach2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

允许程序节点尝试附加到关联的程序接收通知。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugProgramNodeAttach2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 实现位于同一类上实现此接口[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)接口以接收通知的附加操作并提供有机会取消附加操作。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 通过调用来获取此接口`QueryInterface`中的方法[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)对象。 [OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)之前，必须在调用方法[附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)方法，以使程序节点停止附加进程有机会。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 此接口实现以下方法：  
  
|方法|描述|  
|------------|-----------------|  
|[OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)|将附加到相关联的程序或将推迟到 attach 进程[附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)方法。|  
  
## <a name="remarks"></a>备注  
 此接口是不推荐使用的首选的备用[Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)方法。 所有的调试引擎始终加载与`CoCreateInstance`函数中，也就是说，它们实例化外正在调试的程序的地址空间。  
  
 如果以前的实现`IDebugProgramNode2::Attach_V7`只需设置方法`GUID`的正在调试的程序，然后仅[OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)方法需要实现。  
  
 如果以前的实现`IDebugProgramNode2::Attach_V7`方法使用回调接口提供，则该功能需要移动到的实现[附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)方法和`IDebugProgramNodeAttach2`接口没有必须先实现。  
  
## <a name="requirements"></a>要求  
 标头：Msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)   
 [附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)   
 [Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)
