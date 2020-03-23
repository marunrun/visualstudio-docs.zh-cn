---
title: 服务要点 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- services, essentials
ms.assetid: fbe84ad9-efe1-48b1-aba3-b50b90424d47
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8817ca48ff0a3f44a973986a173e647ce89c662c
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301631"
---
# <a name="service-essentials"></a>服务基础知识
服务是两个 VSPackages 之间的协定。 一个 VS 包为另一个 VSPackage 提供了一组特定的接口。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]本身就是一个 VS 包的集合，它向其他 VS 包提供服务。

 例如，可以使用 SVActivityLog 服务获取 IVActivityLog 接口，您可以使用该接口写入活动日志。 有关详细信息，请参阅[：使用活动日志](../../extensibility/how-to-use-the-activity-log.md)。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]还提供一些未注册的内置服务。 VS包可以通过提供服务覆盖来替换内置服务或其他服务。 任何服务只允许一个服务覆盖。

 服务没有可发现性。 因此，您必须知道要使用的服务的服务标识符 （SID），并且必须知道它提供的接口。 服务的参考文档提供此信息。

- 提供服务的 VS 包称为服务提供商。

- 提供给其他 VSPackages 的服务称为全局服务。

- 仅对实现它们的 VSPackage 或其创建的任何对象可用的服务称为本地服务。

- 替换其他包提供的内置服务或服务的服务称为服务覆盖。

- 服务或服务覆盖将按需加载，也就是说，当服务提供程序由另一个 VSPackage 请求时加载它。

- 为了支持按需加载，服务提供商将其全局服务注册到[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。 有关详细信息，请参阅[如何：提供服务](../../extensibility/how-to-provide-a-service.md)。

- 获取服务后，请使用[查询接口](/cpp/atl/queryinterface)（非托管代码）或强制转换（托管代码）来获取所需的接口，例如：

  ```vb
  TryCast(GetService(GetType(SVsActivityLog)), IVsActivityLog)
  ```

  ```csharp
  GetService(typeof(SVsActivityLog)) as IVsActivityLog;
  ```

- 托管代码按服务类型引用服务，而非托管代码按其 GUID 引用服务。

- 加载[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]VSPackage 时，它会将服务提供商传递到 VSPackage，以便 VSPackage 访问全局服务。 这称为 VSPackage 的"坐"。

- VS包可以是它们创建的对象的服务提供商。 例如，窗体可能会向其框架发送颜色服务的请求，这可能会将请求传递给[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。

- 深度嵌套或根本不停靠的托管对象可能要求<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A>直接访问全局服务。

<a name="how-to-use-getglobalservice"></a>

## <a name="use-getglobalservice"></a>使用获取全球服务

有时，您可能需要从尚未设置的工具窗口或控件容器获取服务，或者已使用不知道所需服务的服务提供商。 例如，您可能希望从控件内写入活动日志。 有关这些方案和其他方案的详细信息，请参阅[如何：故障排除服务](../../extensibility/how-to-troubleshoot-services.md)。

您可以通过调用静态<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A>方法获得大多数 Visual Studio 服务。

<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A>依赖于缓存的服务提供商，该提供程序在首次初始化从包派生的任何 VSPackage 时进行定位。 您必须保证满足此条件，否则必须为 null 服务做好准备。

幸运的是，<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A>大多数时候工作正常。

- 如果 VSPackage 提供仅对另一个 VSPackage 已知的服务，则在加载提供服务的 VSPackage 之前，将站点上请求该服务的 VS 包。

- 如果工具窗口由 VSPackage 创建，则在创建工具窗口之前将设置 VSPackage。

- 如果控制容器由 VSPackage 创建的工具窗口承载，则在创建控件容器之前将 VSPackage 设址。

### <a name="to-get-a-service-from-within-a-tool-window-or-control-container"></a>从工具窗口或控件容器内获取服务

- 在构造函数、工具窗口或控件容器中插入此代码：

    ```csharp
    IVsActivityLog log = Package.GetGlobalService(typeof(SVsActivityLog)) as IVsActivityLog;
        if (log == null) return;
    ```

    ```vb
    Dim log As IVsActivityLog = TryCast(Package.GetGlobalService(GetType(SVsActivityLog)), IVsActivityLog)
    If log Is Nothing Then
        Return
    End If
    ```

    此代码获取 SVActivityLog 服务并将其转换为 IVActivityLog 接口，该接口可用于写入活动日志。 有关示例，请参阅[：使用活动日志](../../extensibility/how-to-use-the-activity-log.md)。

## <a name="see-also"></a>另请参阅

- [可用服务的列表](../../extensibility/internals/list-of-available-services.md)
- [使用并提供服务](../../extensibility/using-and-providing-services.md)
- [强制转换和类型转换](/dotnet/csharp/programming-guide/types/casting-and-type-conversions)
- [强制转换](/cpp/cpp/casting)