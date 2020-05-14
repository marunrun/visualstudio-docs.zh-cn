---
title: IDebugGenericParamField |微软文档
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugGenericParamField interface
ms.assetid: ba24f499-5ba7-4c67-83e6-923229b52327
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0b04b0805aec5ecee818fa42e1d76a76cce12b66
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727842"
---
# <a name="idebuggenericparamfield"></a>IDebugGenericParamField
表示托管代码泛型类型的参数。

## <a name="syntax"></a>语法

```
IDebugGenericParamField : IDebugField
```

## <a name="notes-for-implementers"></a>实施者说明
 用于支持泛型。

## <a name="methods"></a>方法
 除了[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)接口上的方法外，此接口还实现了以下方法：

|方法|描述|
|------------|-----------------|
|[ConstraintCount](../../../extensibility/debugger/reference/idebuggenericparamfield-constraintcount.md)|返回与此泛型参数关联的约束数。|
|[GetConstraints](../../../extensibility/debugger/reference/idebuggenericparamfield-getconstraints.md)|检索与此泛型参数关联的约束。|
|[GetFlags](../../../extensibility/debugger/reference/idebuggenericparamfield-getflags.md)|检索此泛型参数的标志。|
|[GetIndex](../../../extensibility/debugger/reference/idebuggenericparamfield-getindex.md)|检索此泛型参数的索引。|
|[GetNameOfFormalParam](../../../extensibility/debugger/reference/idebuggenericparamfield-getnameofformalparam.md)|检索此泛型参数的名称。|
|[GetOwner](../../../extensibility/debugger/reference/idebuggenericparamfield-getowner.md)|检索此泛型参数的类型或方法所有者。|

## <a name="requirements"></a>要求
 标题： Sh.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll
