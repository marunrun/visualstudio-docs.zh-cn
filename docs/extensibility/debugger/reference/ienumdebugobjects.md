---
title: IEnum调试对象 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugObjects
helpviewer_keywords:
- IEnumDebugObjects interface
ms.assetid: 0950364c-6c8a-4b6c-ba37-c6aa359fa72c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c04409fb695613fea5d54b285946c04719fbe5b0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80716264"
---
# <a name="ienumdebugobjects"></a>IEnumDebugObjects
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式赋值器的方式被弃用。 有关实现 CLR 表达式赋值器的信息，请参阅[CLR 表达式赋值器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式赋值器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 此接口表示实现[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)接口的对象的集合。

## <a name="syntax"></a>语法

```
IEnumDebugObjects : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 表达式赋值器实现此接口以提供实现[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)接口的对象集。 请注意，由于[存在 GetCount](../../../extensibility/debugger/reference/ienumdebugobjects-getcount.md)方法，这不是标准 COM 枚举。

## <a name="notes-for-callers"></a>呼叫者备注
- [GetElements](../../../extensibility/debugger/reference/idebugarrayobject-getelements.md)返回此接口。

## <a name="methods-in-vtable-order"></a>按 Vtable 顺序排列的方法
 此接口实现以下方法。

|方法|描述|
|------------|-----------------|
|[下一步](../../../extensibility/debugger/reference/ienumdebugobjects-next.md)|从枚举中检索下一组[IDebugObject 对象](../../../extensibility/debugger/reference/idebugobject.md)。|
|[跳](../../../extensibility/debugger/reference/ienumdebugobjects-skip.md)|跳过指定数量的条目。|
|[重置](../../../extensibility/debugger/reference/ienumdebugobjects-reset.md)|将枚举重置为第一个条目。|
|[克隆](../../../extensibility/debugger/reference/ienumdebugobjects-clone.md)|检索当前枚举的副本。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugobjects-getcount.md)|检索枚举中的条目数。|

## <a name="remarks"></a>备注
 此接口允许调试引擎枚举数组中的一组对象。

## <a name="requirements"></a>要求
 标题： ee.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [GetElements](../../../extensibility/debugger/reference/idebugarrayobject-getelements.md)
