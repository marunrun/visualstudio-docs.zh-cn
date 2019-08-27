---
title: 实现和注册端口提供程序 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], registering port suppliers
- port suppliers, registering
ms.assetid: fb057052-ee16-4272-8e16-a4da5dda0ad4
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 26767193c4489405432054ee94beb195ce8448d7
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66344260"
---
# <a name="implement-and-register-a-port-supplier"></a>实现和注册端口提供程序
端口提供程序的作用是跟踪并提供又管理流程的端口。 当需要创建一个端口时，端口提供程序实例化时使用可以共同创建使用端口供应商的 GUID （会话调试管理器 [SDM] 将使用选定的用户或端口提供程序指定的项目系统端口提供程序）。 然后调用 SDM [CanAddPort](../../extensibility/debugger/reference/idebugportsupplier2-canaddport.md)以查看是否可以添加任何端口。 如果可以添加一个端口，通过调用请求一个新的端口[端口](../../extensibility/debugger/reference/idebugportsupplier2-addport.md)并将其传递[IDebugPortRequest2](../../extensibility/debugger/reference/idebugportrequest2.md)描述该端口。 `AddPort` 返回表示新端口[IDebugPort2](../../extensibility/debugger/reference/idebugport2.md)接口。

## <a name="discussion"></a>讨论
 一个端口创建的端口提供程序，这是与计算机或调试服务器相关联。 服务器枚举通过其端口供应商[EnumPortSuppliers](../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md)方法和端口提供程序枚举通过其端口[EnumPorts](../../extensibility/debugger/reference/idebugportsupplier2-enumports.md)方法。

 除了典型的 COM 注册端口提供程序必须注册与 Visual Studio 通过在特定的注册表位置中将其 CLSID 和名称。 调试 SDK 帮助程序函数调用`SetMetric`处理此工作： 它为每个项进行注册，因此调用一次：

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

 端口提供程序注销本身通过调用`RemoveMetric`（另一个调试 SDK 帮助器函数） 一次针对已注册，因此每个项：

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
> [SDK 帮助程序进行调试](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)`SetMetric`并`RemoveMetric`中定义的静态函数*dbgmetric.h*并编译到*ad2de.lib*。 `metrictypePortSupplier`， `metricCLSID`，并`metricName`中也定义了帮助程序*dbgmetric.h*。

 端口提供程序可以通过方法提供其名称和 GUID [GetPortSupplierName](../../extensibility/debugger/reference/idebugportsupplier2-getportsuppliername.md)并[GetPortSupplierId](../../extensibility/debugger/reference/idebugportsupplier2-getportsupplierid.md)分别。

## <a name="see-also"></a>请参阅
- [实现端口提供程序](../../extensibility/debugger/implementing-a-port-supplier.md)
- [用于调试的 SDK 帮助程序](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
- [端口提供程序](../../extensibility/debugger/port-suppliers.md)