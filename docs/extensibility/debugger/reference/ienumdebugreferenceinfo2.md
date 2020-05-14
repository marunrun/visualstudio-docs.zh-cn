---
title: IEnumDebug参考信息2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugReferenceInfo2
helpviewer_keywords:
- IEnumDebugReferenceInfo2
ms.assetid: 7ed01441-686f-4032-8268-a4c750f19f85
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6132235a7e4789c7d9efe5bae9d7fd531112dab4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80715270"
---
# <a name="ienumdebugreferenceinfo2"></a>IEnumDebugReferenceInfo2
此接口枚举[DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)结构。

## <a name="syntax"></a>语法

```
IEnumDebugReferenceInfo2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 调试引擎 （DE） 实现此接口，作为其对内存中对象的引用的支持的一部分。 仅当支持引用时，才能实现此接口。

## <a name="notes-for-callers"></a>呼叫者备注
 Visual Studio 调用[Enum 儿童](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)以获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IEnumDebugReferenceInfo2`。

|方法|描述|
|------------|-----------------|
|[下一步](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2-next.md)|检索枚举序列中指定数量的[DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)结构。|
|[跳](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2-skip.md)|跳过枚举序列中指定数量的[DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)结构。|
|[重置](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2-reset.md)|将枚举序列重置为开头。|
|[克隆](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2-clone.md)|创建与当前枚举器相同的枚举状态的枚举器。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2-getcount.md)|获取枚举器中[DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)结构的数量。|

## <a name="remarks"></a>备注
 引用本质上是一个类型和地址，而属性是名称、类型和地址。 只要引用的对象存在于内存中，引用就保持不变。 有关详细信息[，请参阅 IDebug 参考 2。](../../../extensibility/debugger/reference/idebugreference2.md)

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)
