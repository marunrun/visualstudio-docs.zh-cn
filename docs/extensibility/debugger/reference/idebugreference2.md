---
title: IDebugReference2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2
helpviewer_keywords:
- IDebugReference2 interface
ms.assetid: 3cfed312-f532-4bce-84a5-1677c14567d7
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 66d35b636516df1052ffa2a70c25da79851dd833
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66329653"
---
# <a name="idebugreference2"></a>IDebugReference2
此接口表示堆栈帧属性或其他某个属性的引用。

> [!NOTE]
> `IDebugReference2` 保留供将来使用，和它的方法应返回所有`E_NOTIMPL`。

## <a name="syntax"></a>语法

```
IDebugReference2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 DE 实现此接口来表示对特定类型的值的引用。 例如，值可能是由于表达式计算、 内存或寄存器和它们的值的列表显示所用的内存上下文的数字值。

## <a name="notes-for-callers"></a>调用方的说明
 调用[GetReference](../../../extensibility/debugger/reference/idebugproperty2-getreference.md)若要获取此接口。 [GetParent](../../../extensibility/debugger/reference/idebugreference2-getparent.md)并[GetDerivedMostReference](../../../extensibility/debugger/reference/idebugreference2-getderivedmostreference.md)也会返回此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IDebugReference2`。

|方法|描述|
|------------|-----------------|
|[GetReferenceInfo](../../../extensibility/debugger/reference/idebugreference2-getreferenceinfo.md)|获取[DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)描述此引用的结构。|
|[SetValueAsString](../../../extensibility/debugger/reference/idebugreference2-setvalueasstring.md)|设置从一个字符串，此引用的值。|
|[SetValueAsReference](../../../extensibility/debugger/reference/idebugreference2-setvalueasreference.md)|设置从另一个引用此引用的值。|
|[EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)|枚举此引用的子级。|
|[GetParent](../../../extensibility/debugger/reference/idebugreference2-getparent.md)|获取此引用的父级。|
|[GetDerivedMostReference](../../../extensibility/debugger/reference/idebugreference2-getderivedmostreference.md)|获取此引用的派生程度最高的引用。|
|[GetMemoryBytes](../../../extensibility/debugger/reference/idebugreference2-getmemorybytes.md)|获取此引用所引用的内存字节数。|
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugreference2-getmemorycontext.md)|获取此引用内存上下文。|
|[GetSize](../../../extensibility/debugger/reference/idebugreference2-getsize.md)|获取大小，以字节为单位，此引用。|
|[SetReferenceType](../../../extensibility/debugger/reference/idebugreference2-setreferencetype.md)|设置此引用类型。|
|[Compare](../../../extensibility/debugger/reference/idebugreference2-compare.md)|将此引用与另一个进行比较。|

## <a name="remarks"></a>备注

> [!NOTE]
> "属性"的这种用法不应混淆，这意味着类的成员变量与尽管`IDebugReference2`可以表示这样的实体。

- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)表示的属性，而`IDebugReference2`表示属性，通常对正在调试的程序中的对象的引用的引用。

 属性和引用之间的主要区别是，属性是指一个对象的命名实例而引用所引用的未命名的实例。 例如，属性可能引用的程序的堆中对象`"a.b"`。 另一个属性可能与相同的对象引用`"c.d"`。 种方式来引用此属性需要`"a.b"`或`"c.d"`处于作用域。 对此相同的对象的引用是无名称;可以对引用的对象，只要该对象的内存有效。

 `IDebugProperty2`接口可以看作具有一个名称、 类型和地址的值。 `IDebugReference2`另一方面只手，可以认为的类型和地址。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [GetReference](../../../extensibility/debugger/reference/idebugproperty2-getreference.md)