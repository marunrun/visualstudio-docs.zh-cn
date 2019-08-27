---
title: IDebugDocumentPosition2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentPosition2
helpviewer_keywords:
- IDebugDocumentPosition2 interface
ms.assetid: 0e838ced-12bb-4efc-b811-2b7c034b77b0
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 36c2fbce0154a5ebefd04ea3614d16db16799510
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66333424"
---
# <a name="idebugdocumentposition2"></a>IDebugDocumentPosition2
此接口表示源文件中的抽象位置。

## <a name="syntax"></a>语法

```
IDebugDocumentPosition2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 Visual Studio 通常实现此接口。 如果它必须提供其自己的源代码，调试引擎 (DE) 还将实现此接口 (为当实现 DE [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)接口)。

## <a name="notes-for-callers"></a>调用方的说明
 此接口作为参数传递[EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md)。 它还提供作为的一部分[BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md) union (具体而言， [BP_LOCATION_CODE_FILE_LINE](../../../extensibility/debugger/reference/bp-location-code-file-line.md)结构)，又是一部分[BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)结构，可用于创建挂起断点。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IDebugDocumentPosition2`。

|方法|描述|
|------------|-----------------|
|[GetFileName](../../../extensibility/debugger/reference/idebugdocumentposition2-getfilename.md)|获取包含此文档位置的源文件的文件名。|
|[GetDocument](../../../extensibility/debugger/reference/idebugdocumentposition2-getdocument.md)|获取包含文档。|
|[IsPositionInDocument](../../../extensibility/debugger/reference/idebugdocumentposition2-ispositionindocument.md)|确定此位置是否包含给定文档中。|
|[GetRange](../../../extensibility/debugger/reference/idebugdocumentposition2-getrange.md)|获取此文档位置的范围。|

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [BP_LOCATION_CODE_FILE_LINE](../../../extensibility/debugger/reference/bp-location-code-file-line.md)