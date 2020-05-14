---
title: IDebug符号搜索事件2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolSearchEvent2
helpviewer_keywords:
- IDebugSymbolSearchEvent2
ms.assetid: 9b946d55-ff85-44eb-b40a-efbf8282eafd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cbe99422e506fb86b0a7e1d9d3242783f3258e6a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80718784"
---
# <a name="idebugsymbolsearchevent2"></a>IDebugSymbolSearchEvent2
此接口由调试引擎 （DE） 发送，以指示已加载正在调试的模块的调试符号。

## <a name="syntax"></a>语法

```
IDebugSymbolSearchEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 DE 实现此接口以报告已加载模块的符号。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须在与此接口相同的对象上实现。 SDM 使用[查询接口](/cpp/atl/queryinterface)访问`IDebugEvent2`接口。

## <a name="notes-for-callers"></a>呼叫者备注
 DE 创建并发送此事件对象以报告已加载模块的符号。 该事件使用 SDM 在连接到正在调试的程序时提供的[IDebugEvent 回调2](../../../extensibility/debugger/reference/idebugeventcallback2.md)回调函数进行发送。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 接口`IDebugSymbolSearchEvent2`公开以下方法。

|方法|描述|
|------------|-----------------|
|[GetSymbolSearchInfo](../../../extensibility/debugger/reference/idebugsymbolsearchevent2-getsymbolsearchinfo.md)|检索有关符号搜索结果的信息。|

## <a name="remarks"></a>备注
 即使符号无法加载，也会发送此事件。 调用`IDebugSymbolSearchEvent2::GetSymbolSearchInfo`允许此事件的处理程序确定模块是否实际具有任何符号。

 Visual Studio 通常使用此事件更新 **"模块"** 窗口中加载的符号的状态。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
