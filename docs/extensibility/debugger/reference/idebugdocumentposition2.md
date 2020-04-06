---
title: IDebug文档位置2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentPosition2
helpviewer_keywords:
- IDebugDocumentPosition2 interface
ms.assetid: 0e838ced-12bb-4efc-b811-2b7c034b77b0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 63742f220d5a776fca180a3f9f7fe9c15e04c66a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731636"
---
# <a name="idebugdocumentposition2"></a>IDebugDocumentPosition2
此接口表示源文件中的抽象位置。

## <a name="syntax"></a>语法

```
IDebugDocumentPosition2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 可视化工作室通常实现此接口。 调试引擎 （DE） 如果必须提供自己的源代码（就像 DE 实现[IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)接口时一样），它也将实现此接口。

## <a name="notes-for-callers"></a>呼叫者备注
 此接口作为参数传递给[EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md)。 它还作为[BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)联合（特别是[BP_LOCATION_CODE_FILE_LINE](../../../extensibility/debugger/reference/bp-location-code-file-line.md)结构）的一部分提供，该联合是[BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)结构的一部分，用于创建挂起的断点。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugDocumentPosition2`。

|方法|描述|
|------------|-----------------|
|[GetFileName](../../../extensibility/debugger/reference/idebugdocumentposition2-getfilename.md)|获取包含此文档位置的源文件的文件名。|
|[GetDocument](../../../extensibility/debugger/reference/idebugdocumentposition2-getdocument.md)|获取包含的文档。|
|[IsPositionInDocument](../../../extensibility/debugger/reference/idebugdocumentposition2-ispositionindocument.md)|确定此位置是否包含在给定文档中。|
|[GetRange](../../../extensibility/debugger/reference/idebugdocumentposition2-getrange.md)|获取此文档位置的范围。|

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [BP_LOCATION_CODE_FILE_LINE](../../../extensibility/debugger/reference/bp-location-code-file-line.md)
