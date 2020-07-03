---
title: 使用 VSPackage 创建扩展 |Microsoft Docs
ms.date: 3/16/2019
ms.topic: how-to
ms.assetid: c0cc5e08-4897-44f2-8309-e3478f1f999e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 68ade2f8d334c1f93349e396d910fa300f6b5417
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903849"
---
# <a name="create-an-extension-with-a-vspackage"></a>使用 VSPackage 创建扩展

本演练演示如何创建 VSIX 项目并添加 VSPackage 项目项。 我们将使用 VSPackage 来获取 UI Shell 服务，以便显示消息框。

## <a name="prerequisites"></a>必备条件

从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 你还可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-vspackage"></a>创建 VSPackage

1. 创建名为**FirstPackage**的 VSIX 项目。 可以通过搜索 "vsix" 在 "**新建项目**" 对话框中找到 VSIX 项目模板。

2. 项目打开时，添加一个名为**FirstPackage**的 Visual Studio 包项模板。 在**解决方案资源管理器**中，右键单击项目节点，然后选择 "**添加**  >  **新项**"。 在 "**添加新项**" 对话框中，选择 " **visual c #**  >  **扩展性**" 并选择 " **visual Studio 包**"。 在窗口底部的 "**名称**" 字段中，将命令文件名更改为*FirstPackage.cs*。

3. 生成项目并启动调试。

    此时将显示 Visual Studio 的实验实例。 有关实验实例的详细信息，请参阅[实验实例](../extensibility/the-experimental-instance.md)。

4. 在实验实例中，打开 "**工具**" "  >  **扩展和更新**" 窗口。 此处应会显示**FirstPackage**扩展。 （如果在 Visual Studio 的工作实例中打开**扩展和更新**，将看不到**FirstPackage**）。

## <a name="load-the-vspackage"></a>加载 VSPackage

此时，不会加载扩展，因为没有任何导致加载的内容。 通常，当你与其 UI 交互（单击菜单命令、打开工具窗口）或指定应在特定 UI 上下文中加载 VSPackage 时，可以加载扩展。 有关加载 Vspackage 和 UI 上下文的详细信息，请参阅[加载 vspackage](../extensibility/loading-vspackages.md)。 在此过程中，我们将向你演示如何在解决方案打开时加载 VSPackage。

1. 打开*FirstPackage.cs*文件。 查找类的声明 `FirstPackage` 。 将现有属性替换为以下属性：

    ```csharp
    [PackageRegistration(UseManagedResourcesOnly = true)]
    [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)] // Info on this package for Help/About
    [ProvideAutoLoad(UIContextGuids80.SolutionExists)]
    [Guid(FirstPackage.PackageGuidString)]
    public sealed class FirstPackage : Package
    ```

2. 让我们添加一条消息，让我们知道 VSPackage 已加载。 我们使用 VSPackage 的 `Initialize()` 方法来执行此操作，因为只有在 VSPackage 被放置后，才能获取 Visual Studio 服务。 （有关获取服务的详细信息，请参阅[如何：获取服务](../extensibility/how-to-get-a-service.md)。）将的 `Initialize()` 方法替换 `FirstPackage` 为获取服务的代码 <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> ，获取 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> 接口，并调用其 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ShowMessageBox%2A> 方法。

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

3. 生成项目并启动调试。 将显示实验实例。

4. 在实验实例中打开解决方案。 应该会看到一个消息框，其中显示了**Initialize （）中的第一个包**。
