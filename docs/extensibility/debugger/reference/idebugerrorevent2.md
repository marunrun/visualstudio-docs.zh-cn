---
title: IDebugErrorevent2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugErrorEvent2
helpviewer_keywords:
- IDebugErrorEvent2 interface
ms.assetid: 275b6f38-b3d4-4cae-8491-491177f524fb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 00fd8b4b42f11d18958f8a969bc4ccd58754ab93
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80730003"
---
# <a name="idebugerrorevent2"></a>IDebugErrorEvent2
此接口指定要向用户报告的错误消息。

## <a name="syntax"></a>语法

```
IDebugErrorEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 调试引擎 （DE） 实现此接口，将错误报告为人可读消息。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口必须在与此接口相同的对象上实现。 SDM 使用[查询接口](/cpp/atl/queryinterface)访问`IDebugEvent2`接口。

## <a name="notes-for-callers"></a>呼叫者备注
 DE 创建并发送此事件对象以报告错误。 该事件使用 SDM 在连接到正在调试的程序时提供的[IDebugEvent 回调2](../../../extensibility/debugger/reference/idebugeventcallback2.md)回调函数进行发送。

## <a name="methods-in-vtable-order"></a>按 Vtable 顺序排列的方法
 此接口实现以下方法：

|方法|描述|
|------------|-----------------|
|`GetErrorMessage`|将错误作为人可读字符串返回。|

## <a name="remarks"></a>备注
 如果调试引擎遇到错误，它可以使用此接口通过 Visual Studio 向用户报告消息。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
