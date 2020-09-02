---
title: 服务基础 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- services, essentials
ms.assetid: fbe84ad9-efe1-48b1-aba3-b50b90424d47
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0e2947cb4cd6a347d8e010340f8689eb1907a28a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80705498"
---
# <a name="service-essentials"></a>服务基础知识
服务是两个 Vspackage 之间的协定。 一个 VSPackage 为其他要使用的 VSPackage 提供一组特定的接口。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 本身是 Vspackage 的集合，可向其他 Vspackage 提供服务。

 例如，你可以使用 SVsActivityLog 服务来获取 IVsActivityLog 接口，该接口可用于写入活动日志。 有关详细信息，请参阅 [如何：使用活动日志](../../extensibility/how-to-use-the-activity-log.md)。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 还提供一些未注册的内置服务。 Vspackage 可以通过提供服务重写来替换内置或其他服务。 对于任何服务，只允许一个服务替代。

 服务没有可发现性。 因此，你必须知道要使用的服务 (SID) 的服务标识符，并且必须知道它提供了哪些接口。 服务的参考文档提供了此信息。

- 提供服务的 Vspackage 称为服务提供商。

- 向其他 Vspackage 提供的服务称为全局服务。

- 仅可用于实现它们的 VSPackage 或为其创建的任何对象的服务称为 "本地服务"。

- 替换内置服务或其他包提供的服务的服务称为服务重写。

- 服务或服务重写是按需加载的，也就是说，当另一个 VSPackage 请求服务提供程序时，将加载该服务提供程序。

- 若要支持按需加载，服务提供商可向注册其全局服务 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 有关详细信息，请参阅 [如何：提供服务](../../extensibility/how-to-provide-a-service.md)。

- 获取服务后，使用 [QueryInterface](/cpp/atl/queryinterface) (非托管代码) 或强制转换 (托管代码) 以获取所需的接口，例如：

  ```vb
  TryCast(GetService(GetType(SVsActivityLog)), IVsActivityLog)
  ```

  ```csharp
  GetService(typeof(SVsActivityLog)) as IVsActivityLog;
  ```

- 托管代码按其类型引用服务，而非托管代码通过其 GUID 来引用服务。

- [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]加载 VSPackage 时，它会将服务提供程序传递到 VSPackage，以便 VSPackage 访问全局服务。 这称为 "选址" VSPackage。

- Vspackage 可以是其创建的对象的服务提供商。 例如，窗体可能会将颜色服务请求发送到其框架，这可能会将请求传递给 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

- 深度嵌套或根本没有放置的托管对象可能会调用 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> 以直接访问全局服务。

<a name="how-to-use-getglobalservice"></a>

## <a name="use-getglobalservice"></a>使用 GetGlobalService

有时，可能需要从工具窗口或控件容器获取未被放置的服务，否则，可能会将其放置在不知道所需服务的服务提供程序中。 例如，你可能想要从控件内写入活动日志。 有关这些方案和其他方案的详细信息，请参阅 [如何：对服务进行故障排除](../../extensibility/how-to-troubleshoot-services.md)。

可以通过调用静态方法获取大多数 Visual Studio 服务 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> 。

<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> 依赖于在第一次从包派生的任何 VSPackage 时初始化的缓存服务提供程序。 必须保证满足此条件，否则应为 null 服务做好准备。

幸运的 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> 是，大多数时间都能正常工作。

- 如果 VSPackage 提供的服务只知道另一个 VSPackage，则请求该服务的 VSPackage 将在加载该服务的 VSPackage 之前放置。

- 如果工具窗口是通过 VSPackage 创建的，则在创建工具窗口之前，VSPackage 被放置。

- 如果控件容器由 VSPackage 所创建的工具窗口承载，则在创建控件容器之前，VSPackage 被放置。

### <a name="to-get-a-service-from-within-a-tool-window-or-control-container"></a>从工具窗口或控件容器中获取服务

- 在构造函数、工具窗口或控件容器中插入以下代码：

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

    此代码获取 SVsActivityLog 服务并将其转换为 IVsActivityLog 接口，该接口可用于写入活动日志。 有关示例，请参阅 [如何：使用活动日志](../../extensibility/how-to-use-the-activity-log.md)。

## <a name="see-also"></a>另请参阅

- [可用服务的列表](../../extensibility/internals/list-of-available-services.md)
- [使用并提供服务](../../extensibility/using-and-providing-services.md)
- [强制转换和类型转换](/dotnet/csharp/programming-guide/types/casting-and-type-conversions)
- [强制转换](/cpp/cpp/casting)
