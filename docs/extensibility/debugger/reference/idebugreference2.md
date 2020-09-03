---
title: IDebugReference2 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80720260"
---
# <a name="idebugreference2"></a>IDebugReference2
此接口表示对堆栈帧属性或某个其他属性的引用。

> [!NOTE]
> `IDebugReference2` 保留以供将来使用，并且其所有方法应返回 `E_NOTIMPL` 。

## <a name="syntax"></a>语法

```
IDebugReference2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 DE 实现此接口，以表示对特定类型的值的引用。 例如，值可以是表达式计算结果的数值、用于显示内存的内存上下文或寄存器及其值的列表。

## <a name="notes-for-callers"></a>调用方说明
 调用 [GetReference](../../../extensibility/debugger/reference/idebugproperty2-getreference.md) 以获取此接口。 [GetParent](../../../extensibility/debugger/reference/idebugreference2-getparent.md) 和 [GetDerivedMostReference](../../../extensibility/debugger/reference/idebugreference2-getderivedmostreference.md) 也返回此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IDebugReference2` 。

|方法|说明|
|------------|-----------------|
|[GetReferenceInfo](../../../extensibility/debugger/reference/idebugreference2-getreferenceinfo.md)|获取描述此引用的 [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md) 结构。|
|[SetValueAsString](../../../extensibility/debugger/reference/idebugreference2-setvalueasstring.md)|设置字符串的此引用的值。|
|[SetValueAsReference](../../../extensibility/debugger/reference/idebugreference2-setvalueasreference.md)|将此引用的值设置为另一个引用。|
|[EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)|枚举此引用的子级。|
|[GetParent](../../../extensibility/debugger/reference/idebugreference2-getparent.md)|获取此引用的父。|
|[GetDerivedMostReference](../../../extensibility/debugger/reference/idebugreference2-getderivedmostreference.md)|获取此引用的派生程度最高的引用。|
|[GetMemoryBytes](../../../extensibility/debugger/reference/idebugreference2-getmemorybytes.md)|获取此引用所引用的内存字节。|
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugreference2-getmemorycontext.md)|获取此引用的内存上下文。|
|[GetSize](../../../extensibility/debugger/reference/idebugreference2-getsize.md)|获取此引用的大小（以字节为单位）。|
|[SetReferenceType](../../../extensibility/debugger/reference/idebugreference2-setreferencetype.md)|设置此引用类型。|
|[比较](../../../extensibility/debugger/reference/idebugreference2-compare.md)|将此引用与另一个引用进行比较。|

## <a name="remarks"></a>备注

> [!NOTE]
> 不应将 "属性" 的用法与这意味着类的成员变量相混淆，尽管 `IDebugReference2` 可以表示此类实体。

- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) 表示属性，而 `IDebugReference2` 表示属性引用，通常是对正在调试的程序中的对象的引用。

 属性和引用之间的主要区别在于，属性是指对象的命名实例，而引用则引用未命名的实例。 例如，属性可以引用程序的堆中的对象 `"a.b"` 。 另一个属性可能引用与相同的对象 `"c.d"` 。 引用此属性的方式要求 `"a.b"` 或 `"c.d"` 在范围内。 对此同一个对象的引用是无值的;只要该对象的内存有效，就可以引用该对象。

 `IDebugProperty2`接口可以被视为具有名称、类型和地址的值。 `IDebugReference2`另一方面，可以被视为一种类型和地址。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [GetReference](../../../extensibility/debugger/reference/idebugproperty2-getreference.md)
