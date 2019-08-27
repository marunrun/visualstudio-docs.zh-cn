---
title: 使用 VSPackage 创建扩展 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: c0cc5e08-4897-44f2-8309-e3478f1f999e
caps.latest.revision: 6
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ddad7149db75aa662f9427a301c04eaf925146f9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68197425"
---
# <a name="creating-an-extension-with-a-vspackage"></a>使用 VSPackage 创建扩展
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本演练演示如何创建 VSIX 项目并添加 VSPackage 项目项。 我们将使用 VSPackage 来获取 UI 外壳服务才能显示一个消息框。  
  
## <a name="prerequisites"></a>系统必备  
 从 Visual Studio 2015 开始，您并不安装 Visual Studio SDK 从下载中心获得。 它是作为 Visual Studio 安装程序中的可选功能包含在内。 此外可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。  
  
## <a name="creating-a-vspackage"></a>创建 VSPackage  
  
1. 创建一个名为的 VSIX 项目**FirstPackage**。 可以查找中的 VSIX 项目模板**新的项目**下的对话框**Visual C# / 可扩展性**。  
  
2. 项目打开后，添加一个名为的 Visual Studio 包项目模板**FirstPackage**。 在中**解决方案资源管理器**，右键单击项目节点并选择**添加 / 新项**。 在中**添加新项**对话框中，转到**Visual C# / 可扩展性**，然后选择**Visual Studio 包**。 在中**名称**在窗口底部字段中，将命令文件名称更改为**FirstPackage.cs**。  
  
3. 生成项目并启动调试。  
  
     将显示 Visual Studio 的实验实例。 有关实验实例的详细信息，请参阅[实验实例](../extensibility/the-experimental-instance.md)。  
  
4. 在实验实例中，打开**工具 / 扩展和更新**窗口。 应会看到**FirstPackage**此处扩展。 (如果您打开**扩展和更新**中的 Visual Studio 工作实例，不会看到**FirstPackage**)。  
  
## <a name="loading-the-vspackage"></a>正在加载 VSPackage  
 此时未加载该扩展，因为没有内容后，即可加载。 在交互 （单击菜单命令，打开工具窗口），其 UI 或通过指定特定 UI 上下文中应该加载 VSPackage 时，通常可以加载扩展。 有关加载 Vspackage 和 UI 上下文的详细信息，请参阅[加载 Vspackage](../extensibility/loading-vspackages.md)。 此过程中，我们将向您介绍如何打开解决方案时加载 VSPackage。  
  
1. 打开 FirstPackage.cs 文件。 查找 FirstPackage 类的声明。 现有属性替换为以下：  
  
    ```csharp  
    [PackageRegistration(UseManagedResourcesOnly = true)]  
    [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)] // Info on this package for Help/About  
    [ProvideAutoLoad(UIContextGuids80.SolutionExists)]  
    [Guid(FirstPackageGuids.PackageGuidString)]  
    public sealed class FirstPackage : Package  
    ```  
  
2. 让我们添加一条消息，让我们知道已加载 VSPackage。 我们使用 VSPackage 的 initialize （） 方法，若要执行此操作，因为只有在 VSPackage 已就位后，你可以获取 Visual Studio 服务。 (有关获取服务的详细信息，请参阅[如何：获取服务](../extensibility/how-to-get-a-service.md)。)FirstPackage initialize （） 方法替换为获取的代码<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>服务，获取<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell>接口，并调用其<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ShowMessageBox%2A>方法。  
  
    ```csharp  
    protected override void Initialize()  
    {  
        base.Initialize();  
  
        IVsUIShell uiShell = (IVsUIShell)GetService(typeof(SVsUIShell));  
        Guid clsid = Guid.Empty;  
        int result;  
        Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure(uiShell.ShowMessageBox(  
            0,  
            ref clsid,  
            "FirstPackage",  
             string.Format(CultureInfo.CurrentCulture, "Inside {0}.Initialize()", this.GetType().FullName),  
            string.Empty,  
            0,  
            OLEMSGBUTTON.OLEMSGBUTTON_OK,  
            OLEMSGDEFBUTTON.OLEMSGDEFBUTTON_FIRST,  
            OLEMSGICON.OLEMSGICON_INFO,  
            0,  
            out result));  
    }  
    ```  
  
3. 生成项目并启动调试。 将显示在实验实例。  
  
4. 在实验实例中打开的解决方案。 你应看到一个消息框，显示**第一个包内 initialize （)** 。
