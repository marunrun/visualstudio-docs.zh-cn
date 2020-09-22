---
title: 实现和注册端口供应商 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840718"
---
# <a name="implementing-and-registering-a-port-supplier"></a>实现和注册端口提供程序
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

端口供应商的角色是跟踪和提供端口，进而管理进程。 需要创建端口时，将使用共同 iopalisserverextension 和端口供应商的 GUID 来实例化端口供应商 (会话调试管理器 [SDM] 将使用用户选择的端口供应商或由项目系统) 指定的端口供应商。 SDM 随后将调用 [CanAddPort](../../extensibility/debugger/reference/idebugportsupplier2-canaddport.md) ，以查看是否可以添加任何端口。 如果可以添加某个端口，则通过调用 [AddPort](../../extensibility/debugger/reference/idebugportsupplier2-addport.md) 并向其传递描述该端口的 [IDebugPortRequest2](../../extensibility/debugger/reference/idebugportrequest2.md) 来请求一个新端口。 `AddPort` 将返回由 [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md) 接口表示的新端口。  
  
## <a name="discussion"></a>讨论 (Discussion)  
 端口由端口供应商创建，后者又与计算机或调试服务器相关联。 服务器可以通过[EnumPortSuppliers](../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md) 方法枚举其端口供应商，端口供应商可以通过 [EnumPorts](../../extensibility/debugger/reference/idebugportsupplier2-enumports.md) 方法枚举其端口。  
  
 除了典型的 COM 注册，端口供应商必须通过将其 CLSID 和名称放入特定的注册表位置，将其自身注册到 Visual Studio。 称为处理此操作的调试 SDK helper 函数 `SetMetric` ：为要注册的每个项调用一次：  
  
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
  
 端口供应商通过调用 `RemoveMetric` 另一个调试 SDK helper 函数) 为注册的每个项 (调用一次来取消注册自身，因此：  
  
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
> [SDK 帮助程序用于调试](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md) `SetMetric` ， `RemoveMetric` 是在 dbgmetric 中定义的、编译到 ad2de 中的静态函数。 `metrictypePortSupplier`、 `metricCLSID` 和帮助程序 `metricName` 也是在 dbgmetric 中定义的。  
  
 端口供应商可以通过 [GetPortSupplierName](../../extensibility/debugger/reference/idebugportsupplier2-getportsuppliername.md) 和 [GetPortSupplierId](../../extensibility/debugger/reference/idebugportsupplier2-getportsupplierid.md)方法分别提供其名称和 GUID。  
  
## <a name="see-also"></a>另请参阅  
 [实现端口供应商](../../extensibility/debugger/implementing-a-port-supplier.md)   
 [SDK 调试帮助程序](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)   
 [端口提供程序](../../extensibility/debugger/port-suppliers.md)
