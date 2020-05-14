---
title: IDebug文档文本2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentText2
helpviewer_keywords:
- IDebugDocumentText2 interface
ms.assetid: e85f50a3-211c-4220-a9f4-789950ba2782
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5b5def7f6cc4ac5ced91ca0a273ce750003dca20
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731563"
---
# <a name="idebugdocumenttext2"></a>IDebugDocumentText2
此接口表示文本文档。

## <a name="syntax"></a>语法

```
IDebugDocumentText2 : IDebugDocument2
```

## <a name="notes-for-implementers"></a>实施者说明
 当需要提供源代码时，调试引擎 （DE） 以文本形式实现此接口。 由于这是最典型的情况，如果 DE 实现[IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)接口，它也应该实现该`IDebugDocumentText2`接口。

## <a name="notes-for-callers"></a>呼叫者备注
 使用`QueryInterface`方法从`IDebugDocument2`接口获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了接口上的方法外`IDebugDocument2`，此接口还实现以下方法：

|方法|描述|
|------------|-----------------|
|[GetSize](../../../extensibility/debugger/reference/idebugdocumenttext2-getsize.md)|检索文档中此位置的文本大小。|
|[获取文本](../../../extensibility/debugger/reference/idebugdocumenttext2-gettext.md)|从文档中的指定位置检索文本。|

## <a name="remarks"></a>备注
 实现此接口的对象还必须实现<xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer>接口，该接口为<xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint>[IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md)对象提供接口。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)
- [IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md)
