---
title: IDebugActivate文档事件2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugActivateDocumentEvent2
helpviewer_keywords:
- IDebugActivateDocumentEvent2 interface
ms.assetid: 6f37edd7-a48c-4b41-b160-dff9be63a284
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f601027ce9e71dff6687bcd6aa1b08f13f5ce0cf
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736615"
---
# <a name="idebugactivatedocumentevent2"></a>IDebugActivateDocumentEvent2
调试引擎 （DE） 使用此接口请求加载文档。

## <a name="syntax"></a>语法

```
IDebugActivateDocumentEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 当 DE 需要打开源文件时，它实现此接口。 此接口仅通过使用脚本解释器或脚本解释器的一部分的调试引擎实现。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须在与此接口相同的对象上实现（SDM 使用[查询接口](/cpp/atl/queryinterface)访问`IDebugEvent2`接口）。

## <a name="notes-for-callers"></a>呼叫者备注
 当 DE 需要打开源文件时，它将创建并发送此事件对象。 该事件使用 SDM 提供的[IDebugEvent 回调2](../../../extensibility/debugger/reference/idebugeventcallback2.md)回调功能在附加到正在调试的程序时发送。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugActivateDocumentEvent2`。

|方法|描述|
|-------------|-----------------|
|[GetDocument](../../../extensibility/debugger/reference/idebugactivatedocumentevent2-getdocument.md)|获取要激活的文档。|
|[GetDocumentContext](../../../extensibility/debugger/reference/idebugactivatedocumentevent2-getdocumentcontext.md)|获取描述文档中位置的文档上下文。|

## <a name="remarks"></a>备注
 使用此接口的典型方案是，如果 HTML 页上的脚本代码中出现分析错误，脚本 DE 会将此接口发送到 SDM，以便显示具有分析错误的文档。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
