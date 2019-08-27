---
title: IDebugPrimitiveTypeField | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPrimitiveTypeField interface
ms.assetid: 73a428fd-797e-4ceb-8392-ba16f1c5226b
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4012b919cffc5e16433567fac283ac731d4d215c
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353270"
---
# <a name="idebugprimitivetypefield"></a>IDebugPrimitiveTypeField
表示基元类型枚举值从[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)接口。

## <a name="syntax"></a>语法

```
IDebugPrimitiveTypeField : IDebugField
```

## <a name="methods"></a>方法
 除了上的方法[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)接口，此接口实现了以下方法：

|方法|描述|
|------------|-----------------|
|[GetPrimitiveType](../../../extensibility/debugger/reference/idebugprimitivetypefield-getprimitivetype.md)|检索与此字段关联的基元类型。|

## <a name="requirements"></a>要求
 标头：Sh.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll