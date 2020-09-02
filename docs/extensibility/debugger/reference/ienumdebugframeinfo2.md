---
title: IEnumDebugFrameInfo2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugFrameInfo2
helpviewer_keywords:
- IEnumDebugFrameInfo2
ms.assetid: 994e30ad-435a-4f9e-9272-d96d9e01099c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0aa67792ced94afd9c4439cbc6ea577e6b85f28b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80716610"
---
# <a name="ienumdebugframeinfo2"></a>IEnumDebugFrameInfo2
此接口枚举 [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) 结构。

## <a name="syntax"></a>语法

```
IEnumDebugFrameInfo2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 调试引擎 (DE) 实现此接口，以提供描述当前调用堆栈的结构的列表。

## <a name="notes-for-callers"></a>调用方说明
 每当正在调试的程序中发生断点、异常或停止时，Visual Studio 都会调用 [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md) 来获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IEnumDebugFrameInfo2` 。

|方法|说明|
|------------|-----------------|
|[下一页](../../../extensibility/debugger/reference/ienumdebugframeinfo2-next.md)|检索枚举序列中指定数量的 [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) 结构。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugframeinfo2-skip.md)|跳过枚举序列中指定数量的 [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) 结构。|
|[重置](../../../extensibility/debugger/reference/ienumdebugframeinfo2-reset.md)|将枚举序列重置到开始处。|
|[克隆](../../../extensibility/debugger/reference/ienumdebugframeinfo2-clone.md)|创建与当前枚举数包含相同枚举状态的枚举数。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugframeinfo2-getcount.md)|获取枚举器中的 [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) 结构数。|

## <a name="remarks"></a>备注
 Visual Studio 获取此接口作为在正在调试的程序上处理断点、异常或用户生成的暂停的第一步。 [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)结构的列表表示当前调用堆栈，当前函数调用位于列表的开头，最早的函数调用位于列表末尾。 每个都 `FRAMEINFO` 表示一个堆栈帧，这是一个可以在其中计算表达式的上下文，以及一个可查看的局部变量。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)
- [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)
