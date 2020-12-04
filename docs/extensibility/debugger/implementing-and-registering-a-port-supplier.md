---
title: 实现和注册端口供应商 |Microsoft Docs
description: 了解如何实现和注册端口供应商，以跟踪和提供管理进程的端口。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: a5bce26a00a525ed93e27b531b36aca1fc04dce4
ms.sourcegitcommit: bbed6a0b41ac4c4a24e8581ff3b34d96345ddb00
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2020
ms.locfileid: "96559922"
---
# <a name="implement-and-register-a-port-supplier"></a>实现并注册端口供应商
端口供应商的角色是跟踪和提供端口，进而管理进程。 需要创建端口时，将使用共同 iopalisserverextension 和端口供应商的 GUID 来实例化端口供应商 (会话调试管理器 [SDM] 将使用用户选择的端口供应商或由项目系统) 指定的端口供应商。 然后，SDM 调用 [CanAddPort](../../extensibility/debugger/reference/idebugportsupplier2-canaddport.md) 来查看是否可以添加任何端口。 如果可以添加某个端口，则通过调用 [AddPort](../../extensibility/debugger/reference/idebugportsupplier2-addport.md) 并向其传递描述该端口的 [IDebugPortRequest2](../../extensibility/debugger/reference/idebugportrequest2.md) 来请求一个新端口。 `AddPort` 返回由 [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md) 接口表示的新端口。

## <a name="discussion"></a>讨论 (Discussion)
 端口由与计算机或调试服务器关联的端口提供程序创建。 服务器通过[EnumPortSuppliers](../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md) 方法枚举其端口供应商，端口供应商通过 [EnumPorts](../../extensibility/debugger/reference/idebugportsupplier2-enumports.md) 方法枚举其端口。

 除了典型的 COM 注册，端口供应商必须通过将其 CLSID 和名称放入特定的注册表位置，将其自身注册到 Visual Studio。 称为处理此操作的调试 SDK helper 函数 `SetMetric` ：为要注册的每个项调用一次：

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

 端口供应商通过调用 `RemoveMetric` 另一个调试 SDK helper 函数) 为注册的每个项 (调用一次来取消注册自身，因此：

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
> [SDK 帮助程序用于调试](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md) `SetMetric` ， `RemoveMetric` 是在 *dbgmetric* 中定义的、编译到 *ad2de* 中的静态函数。 `metrictypePortSupplier`、 `metricCLSID` 和帮助程序 `metricName` 也是在 *dbgmetric* 中定义的。

 端口供应商可以通过 [GetPortSupplierName](../../extensibility/debugger/reference/idebugportsupplier2-getportsuppliername.md) 和 [GetPortSupplierId](../../extensibility/debugger/reference/idebugportsupplier2-getportsupplierid.md)方法分别提供其名称和 GUID。

## <a name="see-also"></a>另请参阅
- [实现端口供应商](../../extensibility/debugger/implementing-a-port-supplier.md)
- [SDK 调试帮助程序](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
- [端口供应商](../../extensibility/debugger/port-suppliers.md)
