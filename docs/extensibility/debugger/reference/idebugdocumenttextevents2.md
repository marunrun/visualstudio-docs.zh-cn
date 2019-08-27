---
title: IDebugDocumentTextEvents2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentTextEvents2
helpviewer_keywords:
- IDebugDocumentTextEvents2 interface
ms.assetid: a10cbb6b-11a8-4056-b42a-2ecebf0e690d
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 56ecf7c81c2be90b975785cc8f07f11af2aa2a7e
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66351352"
---
# <a name="idebugdocumenttextevents2"></a>IDebugDocumentTextEvents2
此接口用于通知 Visual Studio 的调试引擎提供对源文档的更改。

## <a name="syntax"></a>语法

```
IDebugDocumentTextEvents2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 DE 实现此接口以支持对源代码进行更改。 此接口通常实现上实现的相同对象[IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)接口。

## <a name="notes-for-callers"></a>调用方的说明
 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 获取通过调用此接口<xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint.Advise%2A>方法。 <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint>接口获取通过调用<xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer.EnumConnectionPoints%2A>方法。 <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer>接口通过调用[QueryInterface](/cpp/atl/queryinterface)方法[IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IDebugDocumentTextEvents2`。

|方法|描述|
|------------|-----------------|
|[onDestroy](../../../extensibility/debugger/reference/idebugdocumenttextevents2-ondestroy.md)|指示整个文档已被销毁。|
|[onInsertText](../../../extensibility/debugger/reference/idebugdocumenttextevents2-oninserttext.md)|通知调试包到文档中插入文本。|
|[onRemoveText](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onremovetext.md)|通知调试程序包已从文档中删除文本。|
|[onReplaceText](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onreplacetext.md)|通知已替换文本为文档中调试包。|
|[onUpdateTextAttributes](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onupdatetextattributes.md)|通知调试包已在文档文本特性进行了更新。|
|[onUpdateDocumentAttributes](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onupdatedocumentattributes.md)|通知事件的接收方已更新的文档属性。|

## <a name="remarks"></a>备注
 仅提供自己的文档的调试引擎将利用`IDebugDocumentTextEvent2`接口。 此示例将脚本的调试引擎。 在过程中解释脚本，新的源代码可以生成的任何磁盘文件中不存在并仅对 DE 已知。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)
- [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)