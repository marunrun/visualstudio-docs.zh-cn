---
title: 实现和注册端口提供程序 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], registering port suppliers
- port suppliers, registering
ms.assetid: fb057052-ee16-4272-8e16-a4da5dda0ad4
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 377aa88df71fd0d3c42745fe2d3ce3b648191aa4
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63430260"
---
# <a name="implementing-and-registering-a-port-supplier"></a>实现和注册端口提供程序
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

端口提供程序的作用是跟踪并提供又管理流程的端口。 在需要创建一个端口，端口提供程序实例化时使用可以共同创建使用端口供应商的 GUID （端口提供程序用户所选或端口供应商指定的项目系统将使用会话调试管理器 [SDM]）。 然后将调用 SDM [CanAddPort](../../extensibility/debugger/reference/idebugportsupplier2-canaddport.md)以查看是否可以添加任何端口。 如果可以添加一个端口，通过调用请求一个新的端口[端口](../../extensibility/debugger/reference/idebugportsupplier2-addport.md)并将其传递[IDebugPortRequest2](../../extensibility/debugger/reference/idebugportrequest2.md)描述该端口。 `AddPort` 将返回表示新端口[IDebugPort2](../../extensibility/debugger/reference/idebugport2.md)接口。  
  
## <a name="discussion"></a>讨论  
 一个端口创建的端口提供程序，又与计算机或调试服务器相关联。 服务器可以枚举通过其端口供应商[EnumPortSuppliers](../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md)方法和端口提供程序可以枚举通过其端口[EnumPorts](../../extensibility/debugger/reference/idebugportsupplier2-enumports.md)方法。  
  
 除了典型的 COM 注册端口提供程序必须注册与 Visual Studio 通过在特定的注册表位置中将其 CLSID 和名称。 调试 SDK 帮助程序函数调用`SetMetric`处理此工作： 它为每个项进行注册，因此调用一次：  
  
```cpp#  
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
  
```cpp#  
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
> [以便进行调试的 SDK 帮助程序](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)`SetMetric`和`RemoveMetric`dbgmetric.h 中定义并编译为 ad2de.lib 静态函数。 `metrictypePortSupplier`， `metricCLSID`，和`metricName`dbgmetric.h 中也定义了帮助程序。  
  
 端口提供程序可以通过方法提供其名称和 GUID [GetPortSupplierName](../../extensibility/debugger/reference/idebugportsupplier2-getportsuppliername.md)并[GetPortSupplierId](../../extensibility/debugger/reference/idebugportsupplier2-getportsupplierid.md)分别。  
  
## <a name="see-also"></a>请参阅  
 [实现端口提供程序](../../extensibility/debugger/implementing-a-port-supplier.md)   
 [用于调试的 SDK 帮助程序](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)   
 [端口提供程序](../../extensibility/debugger/port-suppliers.md)
