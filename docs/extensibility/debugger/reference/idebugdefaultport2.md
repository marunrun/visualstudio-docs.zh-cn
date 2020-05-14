---
title: IDebug默认端口2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDefaultPort2
helpviewer_keywords:
- IDebugDefaultPort2 interface
ms.assetid: 7b3452af-9a96-4c4c-9946-4339b72d3d7b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f560a3dabefb0a8dede6520dcd8fd47f609a7780
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80732312"
---
# <a name="idebugdefaultport2"></a>IDebugDefaultPort2
此接口提供了几种访问端口服务器和通知工具的方法。

## <a name="syntax"></a>语法

```
IDebugDefaultPort2 : IDebugPort2
```

## <a name="notes-for-implementers"></a>实施者说明
 Visual Studio 实现此接口以表示用于访问程序的调试端口。 如果自定义端口供应商处理远程调试，也可以实现此接口。

## <a name="notes-for-callers"></a>呼叫者备注
 [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)接口上的方法的参数提供此接口。 在[IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)接口上调用[查询接口](/cpp/atl/queryinterface)也可以获取此接口。

## <a name="methods-in-vtable-order"></a>按 Vtable 顺序排列的方法
 除了[在 IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)中定义的方法之外，此接口还实现以下方法：

|方法|描述|
|------------|-----------------|
|[GetPortNotify](../../../extensibility/debugger/reference/idebugdefaultport2-getportnotify.md)|从此端口获取端口通知接口。|
|[GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md)|获取承载此端口的服务器的接口。|
|[QueryIsLocal](../../../extensibility/debugger/reference/idebugdefaultport2-queryislocal.md)|确定此端口是否在本地计算机上运行。|

## <a name="remarks"></a>备注
 名称""`IDebugDefaultPort2`有点用错，因为它不代表默认端口。 它可以称为"IDebugPort3"。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)
