---
title: IDebug动态场 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDynamicField
helpviewer_keywords:
- IDebugDynamicField interface
ms.assetid: caffbd95-7596-4714-84b1-b964e89a78bb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 15f0ddf70849377d37ec74839550de6057b3450c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731313"
---
# <a name="idebugdynamicfield"></a>IDebugDynamicField
此接口表示变量的类型。

## <a name="syntax"></a>语法

```
IDebugDynamicField : IDebugField
```

## <a name="notes-for-implementers"></a>实施者说明
 此接口由符号提供程序实现，作为可在运行时确定的任何类型的基类。 这仅适用于托管代码。

## <a name="notes-for-callers"></a>呼叫者备注
 此接口表示可以从中提取更专用的接口的基类。

## <a name="methods-in-vtable-order"></a>按 Vtable 顺序排列的方法
 此接口不提供除从`IDebugField`继承的方法之外的任何其他方法。

## <a name="requirements"></a>要求
 标题： sh.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
