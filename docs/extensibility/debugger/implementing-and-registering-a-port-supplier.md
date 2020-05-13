---
title: 实施和注册港口供应商 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], registering port suppliers
- port suppliers, registering
ms.assetid: fb057052-ee16-4272-8e16-a4da5dda0ad4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: efa9cdd8740648b66fe7190177b5fe769c4b2539
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738531"
---
# <a name="implement-and-register-a-port-supplier"></a>实施和注册端口供应商
端口供应商的作用是跟踪和供应端口，而端口又管理流程。 当需要创建端口时，将使用 CoCreate 与端口供应商的 GUID 实例化端口供应商（会话调试管理器 [SDM] 将使用用户选择的端口供应商或项目系统指定的端口供应商）。 然后，SDM 调用[CanAddPort](../../extensibility/debugger/reference/idebugportsupplier2-canaddport.md)以查看是否可以添加任何端口。 如果可以添加端口，则通过调用[AddPort](../../extensibility/debugger/reference/idebugportsupplier2-addport.md)并传递描述该端口的[IDebugPortRequest2](../../extensibility/debugger/reference/idebugportrequest2.md)来请求新端口。 `AddPort`返回由[IDebugPort2](../../extensibility/debugger/reference/idebugport2.md)接口表示的新端口。

## <a name="discussion"></a>讨论区
 端口由与计算机或调试服务器关联的端口供应商创建。 服务器通过[EnumPortSuppliers](../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md)方法枚举其端口供应商，端口供应商通过[枚举端口](../../extensibility/debugger/reference/idebugportsupplier2-enumports.md)方法枚举其端口。

 除了典型的 COM 注册之外，端口供应商还必须将其 CLSID 和名称放在特定的注册表位置，从而在 Visual Studio 中注册。 调用`SetMetric`的调试 SDK 帮助器函数处理此杂务：为要注册的每个项目调用一次，因此：

```cpp
SetMetric(metrictypePortSupplier,
          <GUID of your port supplier>,
          metricCLSID,
          <CLSID of your port supplier>,
          false,
          NULL)
SetMetric(metrictypePortSupplier,
          <GUID of your port supplier>,
          metricName,
          <name of your port supplier>,
          false,
          NULL);
```

 端口供应商通过调用`RemoveMetric`（另一个调试 SDK 帮助器函数）对已注册的每个项目一次来取消注册自身，从而：

```cpp
RemoveMetric(metrictypePortSupplier,
             <GUID of your port supplier>,
             metricCLSID,
             NULL);
RemoveMetric(metrictypePortSupplier,
             <GUID of your port supplier>,
             metricName,
             NULL);
```

> [!NOTE]
> [用于调试](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)`SetMetric`的 SDK 帮助`RemoveMetric`器是*dbgmetric.h*中定义的静态函数，并编译为*ad2de.lib*。 `metricCLSID``metricName`和`metrictypePortSupplier`帮助器也在*dbgmetric.h*中定义。

 端口供应商可以通过[GetPort供应商名称](../../extensibility/debugger/reference/idebugportsupplier2-getportsuppliername.md)和[GetPortSupplyId](../../extensibility/debugger/reference/idebugportsupplier2-getportsupplierid.md)的方法分别提供其名称和GUID。

## <a name="see-also"></a>请参阅
- [实施端口供应商](../../extensibility/debugger/implementing-a-port-supplier.md)
- [用于调试的 SDK 帮助器](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
- [港口供应商](../../extensibility/debugger/port-suppliers.md)
