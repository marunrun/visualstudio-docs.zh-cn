---
title: IDebugProperty3 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty3
helpviewer_keywords:
- IDebugProperty3 interface
ms.assetid: 8f9be68d-4490-4eca-8f6b-8a10ed77e226
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8581e8163ab95eac7d49c5deca70c339804aac64
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66348704"
---
# <a name="idebugproperty3"></a>IDebugProperty3
此接口提供以下支持：

- 正在检索任意长度的字符串与属性关联。

- 将与属性关联的唯一 ID。

- 正在检索的属性的自定义查看器的列表。

- 设置属性的值与报告产生的任何错误的功能

## <a name="syntax"></a>语法

```
IDebugProperty3 : IDebugProperty2
```

## <a name="notes-for-implementers"></a>实施者的说明
 调试引擎 (DE) 实现此接口上实现的相同对象[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)长字符串、 属性 Id 和自定义查看器提供支持。

## <a name="notes-for-callers"></a>调用方的说明
 调用[QueryInterface](/cpp/atl/queryinterface)上`IDebugProperty2`接口，以获得此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了继承的方法之外`IDebugProperty2`，则`IDebugProperty3`接口公开以下方法。

|方法|描述|
|------------|-----------------|
|[GetStringCharLength](../../../extensibility/debugger/reference/idebugproperty3-getstringcharlength.md)|返回与属性关联的字符串的长度。|
|[GetStringChars](../../../extensibility/debugger/reference/idebugproperty3-getstringchars.md)|用户提供的缓冲区中返回的字符串。|
|[CreateObjectID](../../../extensibility/debugger/reference/idebugproperty3-createobjectid.md)|创建此属性的唯一 ID。|
|[DestroyObjectID](../../../extensibility/debugger/reference/idebugproperty3-destroyobjectid.md)|销毁此属性的唯一 ID。|
|[GetCustomViewerCount](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md)|返回此属性可以查看使用的自定义查看器数。|
|[GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)|返回此属性可以查看使用的自定义查看器的列表。|
|[SetValueAsStringWithError](../../../extensibility/debugger/reference/idebugproperty3-setvalueasstringwitherror.md)|设置此属性，如果任何出错，则返回一条错误消息的值。|

## <a name="remarks"></a>备注
- [SetValueAsStringWithError](../../../extensibility/debugger/reference/idebugproperty3-setvalueasstringwitherror.md)会话调试管理器 (SDM) 若要设置属性的值是首选的方法。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugCustomViewer](../../../extensibility/debugger/reference/idebugcustomviewer.md)