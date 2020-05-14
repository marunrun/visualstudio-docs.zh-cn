---
title: 如何：获取服务 |微软文档
ms.date: 3/16/2019
ms.topic: conceptual
helpviewer_keywords:
- services, consuming
ms.assetid: 1f000020-8fb7-4e39-8e1e-2e38c7fec3d4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7e8e6f20eaa08d6bb7aaa0cc9e560856daa5959e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710961"
---
# <a name="how-to-get-a-service"></a>如何：获取服务

您通常需要获得 Visual Studio 服务才能访问不同的功能。 通常，Visual Studio 服务提供一个或多个可以使用的接口。 您可以从 VSPackage 获取大多数服务。

任何派生且<xref:Microsoft.VisualStudio.Shell.Package>已正确站点的 VSPackage 都可以请求任何全局服务。 由于`Package`类实现<xref:System.IServiceProvider>，因此派生自`Package`的任何 VSPackage 也是服务提供者。

当 Visual Studio<xref:Microsoft.VisualStudio.Shell.Package>加载 时<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>，它会在<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>初始化期间将对象传递给方法。 这称为*坐 VS*包。 类`Package`包装此服务提供者并提供<xref:Microsoft.VisualStudio.Shell.Package.GetService%2A>获取服务的方法。

## <a name="getting-a-service-from-an-initialized-vspackage"></a>从初始化的 VSPackage 获取服务

1. 每个 Visual Studio 扩展都从 VSIX 部署项目开始，该项目将包含扩展资产。 创建[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]名为 的`GetServiceExtension`VSIX 项目。 您可以通过搜索"vsix"在 **"新项目**"对话框中找到 VSIX 项目模板。

2. 现在添加名为**GetService命令**的自定义命令项模板。 在"**添加新项目"** 对话框中，转到**可视化 C#** > **扩展性**并选择 **"自定义命令**"。 在窗口底部的 **"名称"** 字段中，将命令文件名更改为*GetServiceCommand.cs*。 有关如何创建自定义命令的详细信息，[请使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)

3. 在*GetServiceCommand.cs*中，删除`MenuItemCommand`方法的正文并添加以下代码：

   ```csharp
   IVsActivityLog activityLog = ServiceProvider.GetService(typeof(SVsActivityLog)) as IVsActivityLog;
   if (activityLog == null) return;
   System.Windows.Forms.MessageBox.Show("Found the activity log service.");

   ```

    此代码获取 SVActivityLog 服务并将其转换为<xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog>接口，该接口可用于写入活动日志。 有关示例，请参阅[如何：使用活动日志](../extensibility/how-to-use-the-activity-log.md)。

4. 生成项目并启动调试。 出现实验实例。

5. 在实验实例的 **"工具"** 菜单上，找到 **"调用获取服务命令"** 按钮。 单击此按钮时，应看到一个消息框，其中显示 **"找到活动日志服务"。**

## <a name="getting-a-service-from-a-tool-window-or-control-container"></a>从工具窗口或控件容器获取服务

有时，您可能需要从尚未设置的工具窗口或控件容器获取服务，或者已使用不知道所需服务的服务提供商。 例如，您可能希望从控件内写入活动日志。

静态<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A>方法依赖于缓存的服务提供商，该提供程序在首次对从<xref:Microsoft.VisualStudio.Shell.Package>站点派生的任何 VSPackage 进行初始化时进行初始化。

由于 VSPackage 构造函数是在 VSPackage 进行站点之前调用的，因此在 VSPackage 构造函数中通常无法使用全局服务。 [请参阅如何：为解决方法对服务进行故障排除](../extensibility/how-to-troubleshoot-services.md)。

下面是在工具窗口或其他非 VSPackage 元素中获取服务的方法示例。

```csharp
IVsActivityLog log = Package.GetGlobalService(typeof(SVsActivityLog)) as IVsActivityLog;
if (log == null) return;
```

## <a name="getting-a-service-from-the-dte-object"></a>从 DTE 对象获取服务

您还可以从<xref:EnvDTE.DTEClass>对象获取服务。 但是，您必须从 VSPackage 或调用静态<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A>方法将 DTE 对象作为服务。

DTE 对象实现<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>， 可用于使用<xref:Microsoft.VisualStudio.Shell.ServiceProvider.GetService%2A>来查询服务。

下面了解如何从 DTE 对象获取服务。

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

## <a name="see-also"></a>请参阅

- [如何：提供服务](../extensibility/how-to-provide-a-service.md)
- [使用和提供服务](../extensibility/using-and-providing-services.md)
- [服务要点](../extensibility/internals/service-essentials.md)
