---
title: IDebugDocumentPositionOffset2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugDocumentPositionOffset2 interface
ms.assetid: f1b05db3-50d8-453f-a72f-e68b239236a4
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3793d54249fca1dc867cfe4072326245a67852cb
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66333272"
---
# <a name="idebugdocumentpositionoffset2"></a>IDebugDocumentPositionOffset2
表示源文件中作为字符偏移量的位置。

## <a name="syntax"></a>语法

```
IDebugDocumentPositionOffset2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 通过 IDE 实现和使用的调试引擎。

## <a name="methods"></a>方法
 下表显示的方法`IDebugDocumentPositionOffset2`。

|方法|描述|
|------------|-----------------|
|[GetRange](../../../extensibility/debugger/reference/idebugdocumentpositionoffset2-getrange.md)|检索当前的文档位置的范围。|

## <a name="remarks"></a>备注
 这将返回相同的信息[GetRange](../../../extensibility/debugger/reference/idebugdocumentposition2-getrange.md)但在`char`从文档开头的偏移量。 这提供了文档，它将存在磁盘上，它是字符，而不是通常返回的行和列信息的一维数组。

## <a name="requirements"></a>要求
 标头：Msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)