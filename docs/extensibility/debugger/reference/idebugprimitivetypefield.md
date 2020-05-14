---
title: IDebug原始类型字段 |微软文档
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPrimitiveTypeField interface
ms.assetid: 73a428fd-797e-4ceb-8392-ba16f1c5226b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 07cd3d1a1f80d1c5e816877b7e70a9e65d24d650
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80724267"
---
# <a name="idebugprimitivetypefield"></a>IDebugPrimitiveTypeField
表示[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)接口中的原始类型枚举值。

## <a name="syntax"></a>语法

```
IDebugPrimitiveTypeField : IDebugField
```

## <a name="methods"></a>方法
 除了[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)接口上的方法外，此接口还实现了以下方法：

|方法|描述|
|------------|-----------------|
|[GetPrimitiveType](../../../extensibility/debugger/reference/idebugprimitivetypefield-getprimitivetype.md)|检索与此字段关联的基元类型。|

## <a name="requirements"></a>要求
 标题： Sh.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll
