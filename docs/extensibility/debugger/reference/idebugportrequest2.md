---
title: IDebugPortRequest2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortRequest2
helpviewer_keywords:
- IDebugPortRequest2 interface
ms.assetid: 556e610d-7c4b-44a8-965a-76a9d02b601a
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 83f70a9fe027f004ef3829827ba8af40f7fb72e3
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66340314"
---
# <a name="idebugportrequest2"></a>IDebugPortRequest2
此接口描述一个端口。 此描述用于将端口添加到端口提供程序。

## <a name="syntax"></a>语法

```
IDebugPortRequest2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 Visual Studio 通常实现此接口从端口提供程序获取调试端口的过程中。

## <a name="notes-for-callers"></a>调用方的说明
 此接口传递到[端口](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)创建调试端口。 调用[GetPortRequest](../../../extensibility/debugger/reference/idebugport2-getportrequest.md)返回此接口，表示用于第一个位置中创建该端口的请求。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IDebugPortRequest2`。

|方法|描述|
|------------|-----------------|
|[GetPortName](../../../extensibility/debugger/reference/idebugportrequest2-getportname.md)|获取要创建的端口的名称。|

## <a name="remarks"></a>备注
 通常，调试引擎不与端口提供程序交互，并不会使用此接口。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)
- [GetPortRequest](../../../extensibility/debugger/reference/idebugport2-getportrequest.md)