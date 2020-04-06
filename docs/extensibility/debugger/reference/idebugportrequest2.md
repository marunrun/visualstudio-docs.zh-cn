---
title: IDebugPortRequest2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortRequest2
helpviewer_keywords:
- IDebugPortRequest2 interface
ms.assetid: 556e610d-7c4b-44a8-965a-76a9d02b601a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 163718fda344ba5f3f44ef630b4eba3e5613dc61
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80724789"
---
# <a name="idebugportrequest2"></a>IDebugPortRequest2
此接口描述端口。 此说明用于将端口添加到端口供应商。

## <a name="syntax"></a>语法

```
IDebugPortRequest2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 Visual Studio 通常在从端口供应商获取调试端口的过程中实现此接口。

## <a name="notes-for-callers"></a>呼叫者备注
 此接口传递到[AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)以创建调试端口。 对[GetPortRequest 的](../../../extensibility/debugger/reference/idebugport2-getportrequest.md)调用将返回此接口，表示最初用于创建端口的请求。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugPortRequest2`。

|方法|描述|
|------------|-----------------|
|[GetPortName](../../../extensibility/debugger/reference/idebugportrequest2-getportname.md)|获取要创建的端口的名称。|

## <a name="remarks"></a>备注
 调试引擎通常不与端口供应商交互，并且对此接口没有用处。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)
- [GetPortRequest](../../../extensibility/debugger/reference/idebugport2-getportrequest.md)
