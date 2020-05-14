---
title: IDebug参考2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2
helpviewer_keywords:
- IDebugReference2 interface
ms.assetid: 3cfed312-f532-4bce-84a5-1677c14567d7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 52f655afd35ed316080a3a85ccfae047aa50d87f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80720260"
---
# <a name="idebugreference2"></a>IDebugReference2
此接口表示对堆栈框架属性或其他属性的引用。

> [!NOTE]
> `IDebugReference2`保留以供将来使用，其所有方法应返回`E_NOTIMPL`。

## <a name="syntax"></a>语法

```
IDebugReference2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 DE 实现此接口以表示对特定值类型的引用。 例如，该值可以是表达式计算的结果、用于显示内存的内存上下文或寄存器及其值的列表。

## <a name="notes-for-callers"></a>呼叫者备注
 调用[GetReference](../../../extensibility/debugger/reference/idebugproperty2-getreference.md)以获取此接口。 [获取父级](../../../extensibility/debugger/reference/idebugreference2-getparent.md)和[获取最引用](../../../extensibility/debugger/reference/idebugreference2-getderivedmostreference.md)也返回此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugReference2`。

|方法|描述|
|------------|-----------------|
|[GetReferenceInfo](../../../extensibility/debugger/reference/idebugreference2-getreferenceinfo.md)|获取描述此引用[的DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)结构。|
|[SetValueAsString](../../../extensibility/debugger/reference/idebugreference2-setvalueasstring.md)|从字符串设置此引用的值。|
|[SetValueAsReference](../../../extensibility/debugger/reference/idebugreference2-setvalueasreference.md)|从另一个引用设置此引用的值。|
|[EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)|枚举此引用的子级。|
|[GetParent](../../../extensibility/debugger/reference/idebugreference2-getparent.md)|获取此引用的父项。|
|[GetDerivedMostReference](../../../extensibility/debugger/reference/idebugreference2-getderivedmostreference.md)|获取此引用的最派生引用。|
|[GetMemoryBytes](../../../extensibility/debugger/reference/idebugreference2-getmemorybytes.md)|获取此引用引用的内存字节。|
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugreference2-getmemorycontext.md)|获取此引用的内存上下文。|
|[GetSize](../../../extensibility/debugger/reference/idebugreference2-getsize.md)|获取此引用的大小（以字节为单位）。|
|[SetReferenceType](../../../extensibility/debugger/reference/idebugreference2-setreferencetype.md)|设置此引用类型。|
|[比较](../../../extensibility/debugger/reference/idebugreference2-compare.md)|将此引用与另一个引用进行比较。|

## <a name="remarks"></a>备注

> [!NOTE]
> 不应将"属性"的这种使用与类的成员变量的含义混淆，尽管 可以`IDebugReference2`表示此类实体。

- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)表示一个属性`IDebugReference2`，同时表示对属性的引用，通常是对正在调试的程序中的对象的引用。

 属性和引用之间的主要区别是属性引用对象的命名实例，而引用引用引用未命名的实例。 例如，属性可以引用程序堆中的对象。 `"a.b"` 另一个属性可以引用与`"c.d"`的相同对象。 引用此属性的方式要求 该`"a.b"`或`"c.d"`在作用域中。 对同一对象的引用是无名的;只要该对象的内存有效，就可以引用该对象。

 可以将`IDebugProperty2`接口视为具有名称、类型和地址的值。 另`IDebugReference2`一方面，可以认为是类型和地址。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [获取参考](../../../extensibility/debugger/reference/idebugproperty2-getreference.md)
