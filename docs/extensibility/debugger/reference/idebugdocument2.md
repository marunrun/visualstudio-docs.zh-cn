---
title: IDebugDocument2 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80731989"
---
# <a name="idebugdocument2"></a>IDebugDocument2
此接口表示源文档。

## <a name="syntax"></a>语法

```
IDebugDocument2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 通常实现此接口。 调试引擎 (DE) 还可以在需要提供源代码并且源在磁盘上不存在时实现此接口。  在这种情况下，DE 还会实现 [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md) 和 [IDebugActivateDocumentEvent2](../../../extensibility/debugger/reference/idebugactivatedocumentevent2.md) 接口以及 [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md) 和 [IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md) 接口上的一些其他方法。

## <a name="notes-for-callers"></a>调用方说明
 、、和接口上的方法 `IDebugDocumentContext2` `IDebugDisassemblyStream2` `IDebugDocumentPosition2` `IDebugActivateDocumentEvent2` 返回此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IDebugDocument2` 。

|方法|说明|
|------------|-----------------|
|[GetName](../../../extensibility/debugger/reference/idebugdocument2-getname.md)|获取文档的名称，格式为多个窗体中的一种。|
|[GetDocumentClassID](../../../extensibility/debugger/reference/idebugdocument2-getdocumentclassid.md)|获取文档的类标识符。|

## <a name="remarks"></a>备注
 仅当 DE 提供源代码时才实现此接口。 例如，在 HTML 页上调试脚本时，DE 会提供源代码，因为源是以动态方式下载或生成的，不是作为磁盘文件存在的。 调试传统语言（如 c + +）时，无需实现此接口。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [IsPositionInDocument](../../../extensibility/debugger/reference/idebugdocumentposition2-ispositionindocument.md)
- [GetDocument](../../../extensibility/debugger/reference/idebugactivatedocumentevent2-getdocument.md)
- [GetDocument](../../../extensibility/debugger/reference/idebugdocumentcontext2-getdocument.md)
- [GetDocument](../../../extensibility/debugger/reference/idebugdocumentposition2-getdocument.md)
- [GetDocument](../../../extensibility/debugger/reference/idebugdisassemblystream2-getdocument.md)
