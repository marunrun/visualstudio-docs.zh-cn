---
title: 服务 Essentials |Microsoft Docs
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
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66318686"
---
# <a name="service-essentials"></a>服务基础知识
服务是两个 Vspackage 之间的协定。 一个 VSPackage 提供一组特定的另一个 VSPackage 来使用的接口。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 本身就是向其他 Vspackage 提供服务的 Vspackage 的集合。

 例如，SVsActivityLog 服务可用于获取 IVsActivityLog 接口，它可用于写入活动日志。 有关详细信息，请参阅[如何：使用活动日志](../../extensibility/how-to-use-the-activity-log.md)。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 此外提供了一些内置的服务未注册。 Vspackage 可以通过提供服务重写替换内置或其他服务。 只有一个服务重写被允许的任何服务。

 服务的任何可发现性。 因此，您必须知道服务标识符 (SID) 的一项服务，你想要使用，并且您必须知道它提供了哪些接口。 该服务的参考文档提供了此信息。

- 提供服务的 Vspackage 称为服务提供商。

- 提供给其他 Vspackage 的服务称为全局服务。

- 仅适用于 VSPackage 实现它们，或到它创建任何对象，称为本地服务的服务。

- 替换内置的服务或由其他包，提供服务的服务称为服务重写。

- 按需加载服务或服务重写，它提供的服务请求的另一个 VSPackage 时，它是加载的服务提供程序。

- 若要支持按需加载，服务提供程序注册其全球服务和[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。 有关详细信息，请参阅[如何：提供的服务](../../extensibility/how-to-provide-a-service.md)。

- 获取服务后，使用[QueryInterface](/cpp/atl/queryinterface) （非托管代码） 或强制转换 （托管代码） 来获取所需的接口，例如：

  ```vb
  TryCast(GetService(GetType(SVsActivityLog)), IVsActivityLog)
  ```

  ```csharp
  GetService(typeof(SVsActivityLog)) as IVsActivityLog;
  ```

- 托管的代码引用由其类型的服务，而非托管的代码引用的服务的 GUID。

- 当[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]VSPackage 的加载，将其传递服务提供商到 VSPackage 以使 VSPackage 能够访问全球服务。 这称为"选址"VSPackage。

- Vspackage 可以是服务提供商为他们创建的对象。 例如，窗体可能会将颜色服务的请求发送到其帧中，可能会向其传递请求[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。

- 深度嵌套，或根本没有就位的托管的对象可以调用<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A>直接访问全球服务。

<a name="how-to-use-getglobalservice"></a>

## <a name="use-getglobalservice"></a>使用 GetGlobalService

有时您可能需要从工具窗口中获得的服务或控制已没有已就位，否则使用并不了解所需的服务的服务提供商确定位置的容器。 例如，你可能想要写入活动日志从控件中。 有关这些及其他方案的详细信息，请参阅[如何：排查服务问题](../../extensibility/how-to-troubleshoot-services.md)。

你可以通过调用静态获取大多数 Visual Studio 服务<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A>方法。

<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> 依赖于缓存服务上放置任何 VSPackage 派生自包第一次进行初始化的提供程序。 必须保证，这种情况满足，否则为 null 的服务做好准备。

幸运的是，<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A>大多数情况下正常工作。

- 如果 VSPackage 提供的服务才知道另一个 VSPackage，VSPackage 请求该服务是就位之前提供此服务已加载的 VSPackage。

- 如果 VSPackage 创建工具窗口，则 VSPackage 确定创建工具窗口之前位置。

- 如果控件容器托管的 VSPackage 创建工具窗口，则 VSPackage 确定之前创建的控件容器位置。

### <a name="to-get-a-service-from-within-a-tool-window-or-control-container"></a>若要获取从工具窗口或控件容器中的服务

- 在构造函数、 工具窗口或控件容器中插入此代码：

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

    此代码获取 SVsActivityLog 服务，并将其转换为 IVsActivityLog 接口，它可用于写入活动日志。 有关示例，请参见 [如何：使用活动日志](../../extensibility/how-to-use-the-activity-log.md)。

## <a name="see-also"></a>请参阅

- [可用服务的列表](../../extensibility/internals/list-of-available-services.md)
- [使用并提供服务](../../extensibility/using-and-providing-services.md)
- [强制转换和类型转换](/dotnet/csharp/programming-guide/types/casting-and-type-conversions)
- [强制转换](/cpp/cpp/casting)