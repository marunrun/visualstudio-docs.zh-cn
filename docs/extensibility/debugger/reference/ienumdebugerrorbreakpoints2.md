---
title: IEnum调试错误断点2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugErrorBreakpoints2
helpviewer_keywords:
- IEnumDebugErrorBreakpoints2
ms.assetid: ffdad73d-969a-45ef-9ad1-7f5d3b814018
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ea841a095964b71e301e966bfd0a10c8f7c0c65d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80716881"
---
# <a name="ienumdebugerrorbreakpoints2"></a>IEnumDebugErrorBreakpoints2
此接口枚举与挂起断点关联的错误断点。

## <a name="syntax"></a>语法

```
IEnumDebugErrorBreakpoints2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 调试引擎 （DE） 实现此接口作为其对断点的支持的一部分。

## <a name="notes-for-callers"></a>呼叫者备注
 Visual Studio 调用[CanBind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)以获取此接口，表示无法绑定的断点列表，或[EnumErrorBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)以获取此接口，表示未绑定的断点列表。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IEnumDebugErrorBreakpoints2`。

|方法|描述|
|------------|-----------------|
|[下一步](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2-next.md)|检索枚举序列中指定数量的错误断点。|
|[跳](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2-skip.md)|在枚举序列中跳过指定数量的错误断点。|
|[重置](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2-reset.md)|将枚举序列重置为开头。|
|[克隆](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2-clone.md)|创建与当前枚举器相同的枚举状态的枚举器。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2-getcount.md)|获取枚举器中的错误断点数。|

## <a name="remarks"></a>备注
 此接口包含[IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)接口的列表，每个接口都描述了无法绑定的断点以及为什么无法绑定。 Visual Studio`IEnumDebugErrorBreakpoint2`使用该接口更新 IDE 中显示的断点。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [CanBind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)
- [EnumErrorBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)
- [IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)
