---
title: IDebugTypeFieldBuilder2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugTypeFieldBuilder2 interface
ms.assetid: 23911c5b-2bbf-4734-9976-87a0bd6ea36c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ed34284e373a7d96761aabe5a7f179367649bc0f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80718300"
---
# <a name="idebugtypefieldbuilder2"></a>IDebugTypeFieldBuilder2
扩展 **IDebugTypeFieldBuilder** ，以便能够创建数组类型。

## <a name="syntax"></a>语法

```
IDebugTypeFieldBuilder2 : IDebugTypeFieldBuilder
```

## <a name="notes-for-callers"></a>调用方说明
 此接口可以从符号提供程序获取。

## <a name="methods"></a>方法
 除了 [IDebugTypeFieldBuilder](../../../extensibility/debugger/reference/idebugtypefieldbuilder.md) 接口上的方法，此接口还实现以下方法：

|方法|说明|
|------------|-----------------|
|[CreateArrayOfType](../../../extensibility/debugger/reference/idebugtypefieldbuilder2-createarrayoftype.md)|创建指定类型和大小的数组。|

## <a name="requirements"></a>要求
 标头： Sh。h

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll
