---
title: IDebug地址 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAddress
helpviewer_keywords:
- IDebugAddress interface
ms.assetid: bc709ff7-4966-4f36-9af2-690efe2cea1d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1f281ceb1f305c5774fedbf725f2e6a9481d073d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736591"
---
# <a name="idebugaddress"></a>IDebugAddress
此接口表示项的地址。 它由符号处理程序返回。

## <a name="syntax"></a>语法

```
IDebugAddress : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 符号提供程序实现此接口以表示对象的地址。

## <a name="notes-for-callers"></a>呼叫者备注
 许多接口上的许多方法返回此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 此接口实现以下方法：

|方法|描述|
|------------|-----------------|
|[获取地址](../../../extensibility/debugger/reference/idebugaddress-getaddress.md)|检索描述对象及其位置[DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)结构。|

## <a name="remarks"></a>备注
 符号提供程序返回此接口以表示对象及其在特定作用域中的位置（例如，函数、方法或类）。 此接口从符号提供程序和表达式赋值器的各个方法返回并传递给。 通常，符号提供程序是唯一需要解释此接口内容的实体。

## <a name="requirements"></a>要求
 标题： sh.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)
