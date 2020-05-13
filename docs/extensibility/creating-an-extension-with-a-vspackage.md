---
title: 使用 VS 包创建扩展 |微软文档
ms.date: 3/16/2019
ms.topic: conceptual
ms.assetid: c0cc5e08-4897-44f2-8309-e3478f1f999e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1037ebcc58cc4183e6f02119bc7b46abfc132f52
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739536"
---
# <a name="create-an-extension-with-a-vspackage"></a>使用 VS 包创建扩展

本演练将介绍如何创建 VSIX 项目并添加 VSPackage 项目项。 我们将使用 VSPackage 获取 UI Shell 服务，以便显示消息框。

## <a name="prerequisites"></a>先决条件

从 Visual Studio 2015 开始，您不会从下载中心安装 Visual Studio SDK。 它作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-vspackage"></a>创建 VS 包

1. 创建名为 **"第一包"的**VSIX 项目。 您可以通过搜索"vsix"在 **"新项目**"对话框中找到 VSIX 项目模板。

2. 打开项目时，添加名为**FirstPackage**的可视化工作室包项模板。 在**解决方案资源管理器**中，右键单击项目节点并选择"**添加新** > **项**"。 在 **"添加新项目"** 对话框中，转到**可视化 C#** > **可扩展性**并选择**可视化工作室包**。 在窗口底部的 **"名称"** 字段中，将命令文件名更改为*FirstPackage.cs*。

3. 生成项目并启动调试。

    视觉工作室的实验实例出现。 有关实验实例的详细信息，请参阅[实验实例](../extensibility/the-experimental-instance.md)。

4. 在实验例中，打开 **"工具** > **扩展"和"更新"** 窗口。 您应该在此处查看**第一个包**扩展。 （如果在 Visual Studio 的工作实例中打开**扩展和更新**，则看不到**第一包**）。

## <a name="load-the-vspackage"></a>加载 VS 包

此时，扩展不会加载，因为没有任何内容导致它加载。 通常，在与其 UI 交互时（单击菜单命令、打开工具窗口）或指定 VSPackage 应在特定 UI 上下文中加载时，可以加载扩展。 有关加载 VS 包和 UI 上下文的详细信息，请参阅[加载 VS 包](../extensibility/loading-vspackages.md)。 对于此过程，我们将向您展示如何在打开解决方案时加载 VSPackage。

1. 打开*FirstPackage.cs*文件。 查找类的声明`FirstPackage`。 将现有属性替换为以下属性：

    ```csharp
    [PackageRegistration(UseManagedResourcesOnly = true)]
    [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)] // Info on this package for Help/About
    [ProvideAutoLoad(UIContextGuids80.SolutionExists)]
    [Guid(FirstPackage.PackageGuidString)]
    public sealed class FirstPackage : Package
    ```

2. 让我们添加一条消息，让我们知道 VS 包已加载。 我们使用 VSPackage`Initialize()`的方法执行此操作，因为只有在 VSPackage 已点位后，才能获得 Visual Studio 服务。 （有关获取服务的详细信息，请参阅[如何：获取服务](../extensibility/how-to-get-a-service.md)。`Initialize()`将`FirstPackage`方法替换为获取<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>服务、获取<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell>接口并调用其<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ShowMessageBox%2A>方法的代码。

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

3. 生成项目并启动调试。 出现实验实例。

4. 在实验实例中打开解决方案。 您应该会看到一个消息框，其中显示**第一个包初始化（）**。
