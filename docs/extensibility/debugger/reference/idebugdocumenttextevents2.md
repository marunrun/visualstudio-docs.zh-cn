---
title: IDebug文档文本事件2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentTextEvents2
helpviewer_keywords:
- IDebugDocumentTextEvents2 interface
ms.assetid: a10cbb6b-11a8-4056-b42a-2ecebf0e690d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 44a1736890ac78e7aaf20b4a639b1794fc63b5ac
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731364"
---
# <a name="idebugdocumenttextevents2"></a>IDebugDocumentTextEvents2
此接口用于通知 Visual Studio 有关调试引擎提供的源文档的更改。

## <a name="syntax"></a>语法

```
IDebugDocumentTextEvents2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 DE 实现此接口以支持对源代码进行更改。 此接口通常实现于实现[IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)接口的同一对象上。

## <a name="notes-for-callers"></a>呼叫者备注
 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]通过调用<xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint.Advise%2A>方法获取此接口。 接口<xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint>是从对<xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer.EnumConnectionPoints%2A>方法的调用中获得的。 接口<xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer>是通过在[IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)接口上调用[查询接口](/cpp/atl/queryinterface)方法获得的。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugDocumentTextEvents2`。

|方法|描述|
|------------|-----------------|
|[onDestroy](../../../extensibility/debugger/reference/idebugdocumenttextevents2-ondestroy.md)|指示整个文档已销毁。|
|[onInsertText](../../../extensibility/debugger/reference/idebugdocumenttextevents2-oninserttext.md)|通知调试包文本已插入到文档中。|
|[onRemoveText](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onremovetext.md)|通知调试包文本已从文档中删除。|
|[onReplaceText](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onreplacetext.md)|通知调试包文档中已替换文本。|
|[onUpdateTextAttributes](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onupdatetextattributes.md)|通知调试包文档中的文本属性已更新。|
|[onUpdateDocumentAttributes](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onupdatedocumentattributes.md)|通知接收方事件文档属性已更新。|

## <a name="remarks"></a>备注
 只有调试引擎来提供自己的文档才能利用接口`IDebugDocumentTextEvent2`。 例如脚本调试引擎。 在解释脚本的过程中，可以生成任何磁盘文件中不存在且仅 DE 知道的新源代码。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)
- [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)
