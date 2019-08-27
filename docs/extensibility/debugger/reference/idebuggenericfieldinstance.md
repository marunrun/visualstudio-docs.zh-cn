---
title: IDebugGenericFieldInstance | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugGenericFieldInstance interface
ms.assetid: f68b4761-be8b-4801-9d4b-cde90e01d95e
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 189d670892b50958edff3b256874441aebd72be5
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66330498"
---
# <a name="idebuggenericfieldinstance"></a>IDebugGenericFieldInstance
表示托管的代码的泛型类型的字段的一个实例。

## <a name="syntax"></a>语法

```
IDebugGenericFieldInstance : IUnknown
```

## <a name="methods"></a>方法
 此接口实现以下方法：

|方法|描述|
|------------|-----------------|
|[GetTypeArguments](../../../extensibility/debugger/reference/idebuggenericfieldinstance-gettypearguments.md)|检索此实例的类型参数参数。|
|[TypeArgumentCount](../../../extensibility/debugger/reference/idebuggenericfieldinstance-typeargumentcount.md)|返回此实例的参数自变量类型的数目。|

## <a name="requirements"></a>要求
 标头：Sh.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll