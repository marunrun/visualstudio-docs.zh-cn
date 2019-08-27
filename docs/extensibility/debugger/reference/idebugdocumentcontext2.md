---
title: IDebugDocumentContext2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentContext2
helpviewer_keywords:
- IDebugDocumentContext2
ms.assetid: 2a446c71-8100-4c09-a1cc-fd446bd74030
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fe54a6d3e97fc40f915c42c4aa5397165416b073
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66326646"
---
# <a name="idebugdocumentcontext2"></a>IDebugDocumentContext2
此接口表示源文件文档中的位置。

## <a name="syntax"></a>语法

```
IDebugDocumentContext2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 调试引擎 (DE) 实现此接口作为源代码级别调试的支持的一部分。 除了在源代码中位置，此接口提供了用于比较上下文和源代码文档中导航方法。

## <a name="notes-for-callers"></a>调用方的说明
 方法在多个接口，通常最[GetDocumentContext](../../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md)并[GetDocumentContext](../../../extensibility/debugger/reference/idebugcodecontext2-getdocumentcontext.md)接口，返回此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IDebugDocumentContext2`。

|方法|描述|
|------------|-----------------|
|[GetDocument](../../../extensibility/debugger/reference/idebugdocumentcontext2-getdocument.md)|获取包含此文档上下文中的文档。|
|[GetName](../../../extensibility/debugger/reference/idebugdocumentcontext2-getname.md)|获取包含此文档上下文中的文档的可显示名称。|
|[EnumCodeContexts](../../../extensibility/debugger/reference/idebugdocumentcontext2-enumcodecontexts.md)|检索与此文档上下文关联的所有代码上下文的列表。|
|[GetLanguageInfo](../../../extensibility/debugger/reference/idebugdocumentcontext2-getlanguageinfo.md)|获取与此文档上下文关联的语言。|
|[GetStatementRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md)|获取此文档上下文中的文件语句范围。|
|[GetSourceRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getsourcerange.md)|获取此文档上下文中的文件源范围。|
|[Compare](../../../extensibility/debugger/reference/idebugdocumentcontext2-compare.md)|比较此文档上下文到给定数组的文档上下文。|
|[Seek](../../../extensibility/debugger/reference/idebugdocumentcontext2-seek.md)|按给定数量的语句或行移动文档上下文。|

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [GetDocumentContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getdocumentcontext.md)
- [GetDocumentContext](../../../extensibility/debugger/reference/idebugactivatedocumentevent2-getdocumentcontext.md)
- [GetDocumentContext](../../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md)
- [GetDocumentContext](../../../extensibility/debugger/reference/idebugcodecontext2-getdocumentcontext.md)