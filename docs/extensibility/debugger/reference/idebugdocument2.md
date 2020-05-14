---
title: IDebugDocument2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocument2
helpviewer_keywords:
- IDebugDocument2 interface
ms.assetid: 1bc58426-dbf5-4471-9aad-9d66cd80eef0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4c959c018dd4da0ff088c4fb52c0420de83b4eac
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731989"
---
# <a name="idebugdocument2"></a>IDebugDocument2
此接口表示源文档。

## <a name="syntax"></a>语法

```
IDebugDocument2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]通常实现此接口。 调试引擎 （DE） 也可以实现此接口，当它需要提供源代码，并且磁盘上不存在源代码时。  在这种情况下，DE 还将实现[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)和[IDebugActivateDocumentEvent2](../../../extensibility/debugger/reference/idebugactivatedocumentevent2.md)接口，以及[IDebugdisassemblystream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)和[IDebugDocumentE2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)接口上的一些其他方法。

## <a name="notes-for-callers"></a>呼叫者备注
 上`IDebugDocumentContext2`的方法`IDebugDisassemblyStream2`，`IDebugDocumentPosition2`和`IDebugActivateDocumentEvent2`接口返回此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugDocument2`。

|方法|描述|
|------------|-----------------|
|[GetName](../../../extensibility/debugger/reference/idebugdocument2-getname.md)|以几种形式之一获取文档的名称。|
|[GetDocumentClassID](../../../extensibility/debugger/reference/idebugdocument2-getdocumentclassid.md)|获取文档的类标识符。|

## <a name="remarks"></a>备注
 仅当 DE 提供源代码时，才实现此接口。 例如，当您在 HTML 页上调试脚本时，DE 提供源代码，因为源代码是动态下载或生成的，并且不存在为磁盘文件。 调试传统语言（如C++）时，不需要实现此接口。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [IsPositionInDocument](../../../extensibility/debugger/reference/idebugdocumentposition2-ispositionindocument.md)
- [GetDocument](../../../extensibility/debugger/reference/idebugactivatedocumentevent2-getdocument.md)
- [GetDocument](../../../extensibility/debugger/reference/idebugdocumentcontext2-getdocument.md)
- [GetDocument](../../../extensibility/debugger/reference/idebugdocumentposition2-getdocument.md)
- [GetDocument](../../../extensibility/debugger/reference/idebugdisassemblystream2-getdocument.md)
