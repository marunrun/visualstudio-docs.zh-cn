---
title: 如何：获取服务 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- services, consuming
ms.assetid: 1f000020-8fb7-4e39-8e1e-2e38c7fec3d4
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 46ef86b8cde506aad3e00aa6b5dbc6470c0087de
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68204179"
---
# <a name="how-to-get-a-service"></a>如何：获取服务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通常需要获取 Visual Studio 服务访问不同的功能。 一般情况下，Visual Studio 服务提供了一个或多个接口，可以使用。 你可以从 VSPackage 获取大多数服务。  
  
 派生自任何 VSPackage<xref:Microsoft.VisualStudio.Shell.Package>并已正确放置的任何全局服务可以要求。 因为程序包类实现<xref:System.IServiceProvider>，从包派生而来的任何 VSPackage 也是服务提供程序。  
  
 Visual Studio 加载时<xref:Microsoft.VisualStudio.Shell.Package>，它将传递<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>对象传递给<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A>在初始化过程中的方法。 这称为*选址*VSPackage。 包类封装该服务提供程序，并提供了<xref:Microsoft.VisualStudio.Shell.Package.GetService%2A>用于获取服务的方法。  
  
## <a name="getting-a-service-from-an-initialized-vspackage"></a>从已初始化的 VSPackage 中获取服务  
  
1. 每个 Visual Studio 扩展开始于 VSIX 部署项目，它将包含扩展资产。 创建[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]VSIX 项目名为`GetServiceExtension`。 可以查找中的 VSIX 项目模板**新的项目**下的对话框**Visual C# / 可扩展性**。  
  
2. 现在，添加名为的自定义命令项模板**GetServiceCommand**。 在中**添加新项**对话框中，转到**Visual C# / 可扩展性**，然后选择**自定义命令**。 在中**名称**在窗口底部字段中，将命令文件名称更改为**GetServiceCommand.cs**。 详细了解如何创建自定义命令[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)  
  
3. 在 GetServiceCommand.cs，MenuItemCommand 方法的主体中删除并添加以下代码：  
  
    ```csharp  
    IVsActivityLog activityLog = ServiceProvider.GetService(typeof(SVsActivityLog)) as IVsActivityLog;  
    if (activityLog == null) return;  
    System.Windows.Forms.MessageBox.Show("Found the activity log service.");  
  
    ```  
  
     此代码获取 SVsActivityLog 服务并将强制转换到<xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog>接口，可用于写入活动日志。 有关示例，请参见 [如何：使用活动日志](../extensibility/how-to-use-the-activity-log.md)。  
  
4. 生成项目并启动调试。 将显示在实验实例。  
  
5. 在实验实例工具菜单中，找到**调用 GetServiceCommand**按钮。 当单击此按钮时，您应看到一个消息框，显示**找到活动日志服务。**  
  
## <a name="getting-a-service-from-a-tool-window-or-control-container"></a>从工具窗口或控件容器中获取服务  
 有时您可能需要从工具窗口中获得的服务或控制已没有已就位，否则使用并不了解所需的服务的服务提供商确定位置的容器。 例如，你可能想要写入活动日志从控件中。  
  
 静态<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A>方法依赖于任何 VSPackage 派生自第一次进行初始化的缓存的服务提供商<xref:Microsoft.VisualStudio.Shell.Package>确定位置。  
  
 因为之前确定位置 VSPackage 调用 VSPackage 构造函数，全球服务不可用通常从 VSPackage 构造函数内。 请参阅[如何：排查服务问题](../extensibility/how-to-troubleshoot-services.md)的一种解决方法。  
  
 下面是方法的在工具窗口或其他非 VSPackage 元素中获取服务的示例。  
  
```csharp  
IVsActivityLog log = Package.GetGlobalService(typeof(SVsActivityLog)) as IVsActivityLog;  
if (log == null) return;  
```  
  
## <a name="getting-a-service-from-the-dte-object"></a>从 DTE 对象获取服务  
 你还可以获取从服务<xref:EnvDTE.DTEClass>对象。 但是，你必须获取 DTE 对象作为一项服务从 VSPackage 或通过调用静态<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A>方法。  
  
 DTE 对象实现<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>，您可以使用该查询通过使用服务<xref:Microsoft.VisualStudio.Shell.ServiceProvider.GetService%2A>。  
  
 下面介绍了如何从 DTE 对象获取服务。  
  
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
 [如何：提供的服务](../extensibility/how-to-provide-a-service.md)   
 [使用并提供服务](../extensibility/using-and-providing-services.md)   
 [服务基础知识](../extensibility/internals/service-essentials.md)
