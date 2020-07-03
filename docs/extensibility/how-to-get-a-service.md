---
title: 如何：获取服务 |Microsoft Docs
ms.date: 3/16/2019
ms.topic: how-to
helpviewer_keywords:
- services, consuming
ms.assetid: 1f000020-8fb7-4e39-8e1e-2e38c7fec3d4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a401103112096a1089b59ba3733d19480f93e891
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905829"
---
# <a name="how-to-get-a-service"></a>如何：获取服务

通常需要获取 Visual Studio 服务才能访问不同的功能。 通常，Visual Studio 服务提供一个或多个可以使用的接口。 你可以从 VSPackage 获取大多数服务。

派生自且已正确放置的任何 VSPackage <xref:Microsoft.VisualStudio.Shell.Package> 都可以请求任何全局服务。 由于 `Package` 类实现 <xref:System.IServiceProvider> ，从派生的任何 VSPackage `Package` 也是服务提供程序。

当 Visual Studio 加载时 <xref:Microsoft.VisualStudio.Shell.Package> ，它会 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> 在初始化期间将对象传递给 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> 方法。 这称为 VSPackage 的*选址*。 `Package`类包装此服务提供程序，并提供 <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> 用于获取服务的方法。

## <a name="getting-a-service-from-an-initialized-vspackage"></a>从已初始化的 VSPackage 获取服务

1. 每个 Visual Studio 扩展都从一个 VSIX 部署项目开始，该项目将包含扩展资产。 创建一个 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 名为的 VSIX 项目 `GetServiceExtension` 。 可以通过搜索 "vsix" 在 "**新建项目**" 对话框中找到 VSIX 项目模板。

2. 现在，添加一个名为**GetServiceCommand**的自定义命令项模板。 在 "**添加新项**" 对话框中，选择 " **Visual c #**  >  **扩展性**" 并选择 "**自定义命令**"。 在窗口底部的 "**名称**" 字段中，将命令文件名更改为*GetServiceCommand.cs*。 有关如何创建自定义命令的详细信息，请[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)

3. 在*GetServiceCommand.cs*中，删除方法的正文 `MenuItemCommand` 并添加以下代码：

   ```csharp
   IVsActivityLog activityLog = ServiceProvider.GetService(typeof(SVsActivityLog)) as IVsActivityLog;
   if (activityLog == null) return;
   System.Windows.Forms.MessageBox.Show("Found the activity log service.");

   ```

    此代码将获取一个 SVsActivityLog 服务，并将其转换为一个 <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog> 接口，该接口可用于写入活动日志。 有关示例，请参阅[如何：使用活动日志](../extensibility/how-to-use-the-activity-log.md)。

4. 生成项目并启动调试。 将显示实验实例。

5. 在实验实例的 "**工具**" 菜单中，找到 "**调用 GetServiceCommand** " 按钮。 单击此按钮时，应会看到一个消息框，其中显示 **"活动日志服务"。**

## <a name="getting-a-service-from-a-tool-window-or-control-container"></a>从工具窗口或控件容器获取服务

有时，可能需要从工具窗口或控件容器获取未被放置的服务，否则，可能会将其放置在不知道所需服务的服务提供程序中。 例如，你可能想要从控件内写入活动日志。

静态 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> 方法依赖于缓存的服务提供程序，该提供程序在第一次从派生的任何 VSPackage 时进行初始化 <xref:Microsoft.VisualStudio.Shell.Package> 。

由于 VSPackage 构造函数是在 VSPackage 被放置之前调用的，因此，在 VSPackage 构造函数中通常不能使用全局服务。 有关解决方法，请参阅[如何：解决服务问题](../extensibility/how-to-troubleshoot-services.md)。

下面是在工具窗口或其他非 VSPackage 元素中获取服务的方法的示例。

```csharp
IVsActivityLog log = Package.GetGlobalService(typeof(SVsActivityLog)) as IVsActivityLog;
if (log == null) return;
```

## <a name="getting-a-service-from-the-dte-object"></a>从 DTE 对象获取服务

还可以从对象获取服务 <xref:EnvDTE.DTEClass> 。 但是，必须从 VSPackage 或通过调用静态方法获取 DTE 对象作为服务 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> 。

DTE 对象实现 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> ，可用于通过使用查询服务 <xref:Microsoft.VisualStudio.Shell.ServiceProvider.GetService%2A> 。

下面介绍如何从 DTE 对象获取服务。

```csharp
// Start with the DTE object, for example: 
// using EnvDTE;
// DTE dte = (DTE)GetService(typeof(DTE));

ServiceProvider sp = new ServiceProvider((Microsoft.VisualStudio.OLE.Interop.IServiceProvider)dte);
if (sp != null)
{
    IVsActivityLog log = sp.GetService(typeof(SVsActivityLog)) as IVsActivityLog;
    if (log != null)
    {
        System.Windows.Forms.MessageBox.Show("Found the activity log service.");
    }
}
```

## <a name="see-also"></a>另请参阅

- [如何：提供服务](../extensibility/how-to-provide-a-service.md)
- [使用并提供服务](../extensibility/using-and-providing-services.md)
- [服务基础](../extensibility/internals/service-essentials.md)
