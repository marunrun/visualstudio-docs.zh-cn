---
title: IEnum调试自定义属性 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumCustomAttributes
helpviewer_keywords:
- IEnumDebugCustomAttributes interface
ms.assetid: 11aa768d-1852-44d6-9de3-17f9bafaded2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7f8b521432124267d3f0e179d3a889fb599fa99d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80717127"
---
# <a name="ienumdebugcustomattributes"></a>IEnumDebugCustomAttributes
枚举自定义属性。

## <a name="syntax"></a>语法

```
IEnumCustomAttributes : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 符号提供程序实现此接口以支持自定义属性（通过[IDebugCustom属性](../../../extensibility/debugger/reference/idebugcustomattribute.md)接口）。

## <a name="notes-for-callers"></a>呼叫者备注
- [枚举自定义属性](../../../extensibility/debugger/reference/idebugcustomattributequery2-enumcustomattributes.md)返回此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IEnumDebugCustomAttributes`。

|方法|描述|
|------------|-----------------|
|[下一步](../../../extensibility/debugger/reference/ienumdebugcustomattributes-next.md)|检索枚举序列中指定数量的自定义属性。|
|[跳](../../../extensibility/debugger/reference/ienumdebugcustomattributes-skip.md)|在枚举序列中跳过指定数量的自定义属性。|
|[重置](../../../extensibility/debugger/reference/ienumdebugcustomattributes-reset.md)|将枚举序列重置为开头。|
|[克隆](../../../extensibility/debugger/reference/ienumdebugcustomattributes-clone.md)|创建与当前枚举器相同的枚举状态的枚举器。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugcustomattributes-getcount.md)|获取枚举器中的自定义属性数。|

## <a name="requirements"></a>要求
 标题： sh.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [EnumCustomAttributes](../../../extensibility/debugger/reference/idebugcustomattributequery2-enumcustomattributes.md)
- [IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)
