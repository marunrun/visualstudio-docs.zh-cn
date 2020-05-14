---
title: IDebug属性3 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty3
helpviewer_keywords:
- IDebugProperty3 interface
ms.assetid: 8f9be68d-4490-4eca-8f6b-8a10ed77e226
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d2819724c204631112fd1a3e827126c4bc176972
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721041"
---
# <a name="idebugproperty3"></a>IDebugProperty3
此接口支持：

- 检索与该属性关联的任意长字符串。

- 将唯一 ID 与 属性关联。

- 检索属性的自定义查看器列表。

- 设置属性的值，并能够报告任何生成的错误

## <a name="syntax"></a>语法

```
IDebugProperty3 : IDebugProperty2
```

## <a name="notes-for-implementers"></a>实施者说明
 调试引擎 （DE） 在实现[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)的同一对象上实现此接口，以支持长字符串、属性 IT 和自定义查看器。

## <a name="notes-for-callers"></a>呼叫者备注
 在`IDebugProperty2`接口上调用[查询接口](/cpp/atl/queryinterface)以获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了从`IDebugProperty2`继承的方法外，`IDebugProperty3`接口还公开以下方法。

|方法|描述|
|------------|-----------------|
|[GetStringCharLength](../../../extensibility/debugger/reference/idebugproperty3-getstringcharlength.md)|返回与属性关联的字符串的长度。|
|[GetStringChars](../../../extensibility/debugger/reference/idebugproperty3-getstringchars.md)|返回用户提供的缓冲区中的字符串。|
|[CreateObjectID](../../../extensibility/debugger/reference/idebugproperty3-createobjectid.md)|为此属性创建唯一 ID。|
|[DestroyObjectID](../../../extensibility/debugger/reference/idebugproperty3-destroyobjectid.md)|销毁此属性的唯一 ID。|
|[GetCustomViewerCount](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md)|返回可以使用此属性查看的自定义查看器数。|
|[GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)|返回可以使用此属性查看的自定义查看器的列表。|
|[SetValueAsStringWithError](../../../extensibility/debugger/reference/idebugproperty3-setvalueasstringwitherror.md)|设置此属性的值，如果出现问题，将返回错误消息。|

## <a name="remarks"></a>备注
- [SetValueAsStringWithError](../../../extensibility/debugger/reference/idebugproperty3-setvalueasstringwitherror.md)是会话调试管理器 （SDM） 设置属性值的首选方式。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugCustomViewer](../../../extensibility/debugger/reference/idebugcustomviewer.md)
