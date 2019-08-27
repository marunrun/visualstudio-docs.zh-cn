---
title: IDebugTypeFieldBuilder | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugTypeFieldBuilder interface
ms.assetid: 2dfed0be-6972-4bec-baec-f0b78df9ef97
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 165bbf6326bee67718c4c2ae44933d1b21b8252c
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66319791"
---
# <a name="idebugtypefieldbuilder"></a>IDebugTypeFieldBuilder
表示创建表示一种类型的字段的功能。

## <a name="syntax"></a>语法

```
IDebugTypeFieldBuilder : IUnknown
```

## <a name="notes-for-callers"></a>调用方的说明
 此接口是从符号提供程序获取的。

## <a name="methods"></a>方法
 此接口实现以下方法：

|方法|描述|
|------------|-----------------|
|[CreatePrimitive](../../../extensibility/debugger/reference/idebugtypefieldbuilder-createprimitive.md)|创建表示基元类型的对象。|
|[CreatePointerToType](../../../extensibility/debugger/reference/idebugtypefieldbuilder-createpointertotype.md)|创建为指定类型的指针。|

## <a name="requirements"></a>要求
 标头：Sh.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll