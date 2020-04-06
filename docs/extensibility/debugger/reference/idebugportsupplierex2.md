---
title: IDebugPort供应商Ex2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPortSupplierEx2 interface
ms.assetid: dae0050a-a50a-4f35-bfbd-e538f537b20f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 26387618b320ed56ce754e64698fbb1c4223f2f6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80724320"
---
# <a name="idebugportsupplierex2"></a>IDebugPortSupplierEx2
支持端口供应商选择核心服务器并与之交互。

## <a name="syntax"></a>语法

```
IDebugPortSupplierEx2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 自定义端口供应商实现此接口，以便可以选择要使用的核心服务器。

## <a name="methods"></a>方法
 下表显示了**IDebugPort供应商Ex2**的方法。

|方法|描述|
|------------|-----------------|
|[SetServer](../../../extensibility/debugger/reference/idebugportsupplierex2-setserver.md)|设置端口供应商的核心服务器。|

## <a name="requirements"></a>要求
 标题： 波特普里夫.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
- [IDebugPortSupplier3](../../../extensibility/debugger/reference/idebugportsupplier3.md)
