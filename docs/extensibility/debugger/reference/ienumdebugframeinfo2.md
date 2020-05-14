---
title: IEnumDebugFrameInfo2 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80716610"
---
# <a name="ienumdebugframeinfo2"></a>IEnumDebugFrameInfo2
此接口枚举[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)结构。

## <a name="syntax"></a>语法

```
IEnumDebugFrameInfo2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 调试引擎 （DE） 实现此接口，以提供描述当前调用堆栈的结构列表。

## <a name="notes-for-callers"></a>呼叫者备注
 Visual Studio 调用[EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)获取此接口，每当正在调试的程序中出现断点、异常或停止时。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IEnumDebugFrameInfo2`。

|方法|描述|
|------------|-----------------|
|[下一步](../../../extensibility/debugger/reference/ienumdebugframeinfo2-next.md)|检索枚举序列中指定数量的[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)结构。|
|[跳](../../../extensibility/debugger/reference/ienumdebugframeinfo2-skip.md)|在枚举序列中跳过指定数量的[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)结构。|
|[重置](../../../extensibility/debugger/reference/ienumdebugframeinfo2-reset.md)|将枚举序列重置为开头。|
|[克隆](../../../extensibility/debugger/reference/ienumdebugframeinfo2-clone.md)|创建与当前枚举器相同的枚举状态的枚举器。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugframeinfo2-getcount.md)|获取枚举器中的[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)结构数。|

## <a name="remarks"></a>备注
 Visual Studio 获取此接口是处理正在调试的程序上的断点、异常或用户生成的暂停的第一步。 [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)结构列表表示当前调用堆栈，当前函数调用位于列表的开头，最旧的函数调用位于列表的末尾。 每个`FRAMEINFO`表示一个堆栈帧，可以在其中计算表达式并查看局部变量。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)
- [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)
