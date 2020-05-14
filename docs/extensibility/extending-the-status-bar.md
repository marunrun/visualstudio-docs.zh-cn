---
title: 扩展状态栏 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- status bars, about status bars
- status bars, overview
ms.assetid: f955115c-4c5f-45ec-b41b-365868c5ec0c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: aa62326d82d81f7ee4d10a838209364355cc488e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711545"
---
# <a name="extend-the-status-bar"></a>扩展状态栏
您可以使用 IDE 底部的可视化工作室状态栏来显示信息。

 扩展状态栏时，可以在四个区域中显示信息和 UI：反馈区域、进度栏、动画区域和设计器区域。 反馈区域允许您显示文本并突出显示显示的文本。 进度栏显示短运行操作（如保存文件）的增量进度。 动画区域显示连续循环动画，用于长时间运行的操作或不确定长度的操作，例如在解决方案中生成多个项目。 设计器区域显示光标位置的行号和列号。

 您可以使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbar>接口（从服务）<xref:Microsoft.VisualStudio.Shell.Interop.SVsStatusbar>获取状态栏。 此外，任何位于窗口框架上的对象都可以通过实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser>接口注册为状态栏客户端对象。 每当激活窗口时，Visual Studio 都会查询该窗口中为`IVsStatusbarUser`接口设置的对象。 如果找到，它将调用返回<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser.SetInfo%2A>的接口上的方法，并且对象可以从该方法内更新状态栏。 例如，文档窗口可以使用 方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser.SetInfo%2A>在设计器区域中的信息变为活动时更新它们。

 以下过程假定您了解如何创建 VSIX 项目和添加自定义菜单命令。 有关详细信息，请参阅[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

## <a name="modify-the-status-bar"></a>修改状态栏
 此过程演示如何设置和获取文本、显示静态文本以及突出显示状态栏的反馈区域中显示的文本。

### <a name="read-and-write-to-the-status-bar"></a>读取并写入状态栏

1. 创建名为**TestStatusBar 扩展的**VSIX 项目，并添加名为**TestStatusBar 命令的菜单命令**。

2. 在*TestStatusBarCommand.cs*中，将命令处理程序方法代码`MenuItemCallback`（） 替换为以下内容：

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        IVsStatusbar statusBar = (IVsStatusbar)ServiceProvider.GetService(typeof(SVsStatusbar));

        // Make sure the status bar is not frozen
        int frozen;

        statusBar.IsFrozen(out frozen);

        if (frozen != 0)
        {
            statusBar.FreezeOutput(0);
        }

        // Set the status bar text and make its display static.
        statusBar.SetText("We just wrote to the status bar.");

        // Freeze the status bar.
        statusBar.FreezeOutput(1);

        // Get the status bar text.
        string text;
        statusBar.GetText(out text);
        System.Windows.Forms.MessageBox.Show(text);

        // Clear the status bar text.
        statusBar.FreezeOutput(0);
        statusBar.Clear();
    }
    ```

3. 编译代码并开始调试。

4. 打开可视化工作室实验实例中的 **"工具**"菜单。 单击 **"调用测试状态栏命令"按钮**。

     您应该看到状态栏中的文本现在显示 **"我们刚刚写入状态栏"。** 显示的消息框具有相同的文本。

### <a name="update-the-progress-bar"></a>更新进度栏

1. 在此过程中，我们将演示如何初始化和更新进度栏。

2. 打开*TestStatusBarCommand.cs*文件，`MenuItemCallback`并将该方法替换为以下代码：

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        IVsStatusbar statusBar = (IVsStatusbar)ServiceProvider.GetService(typeof(SVsStatusbar));
        uint cookie = 0;
        string label = "Writing to the progress bar";

        // Initialize the progress bar.
        statusBar.Progress(ref cookie, 1, "", 0, 0);

        for (uint i = 0, total = 20; i <= total; i++)
        {
            // Display progress every second.
            statusBar.Progress(ref cookie, 1, label, i, total);
            System.Threading.Thread.Sleep(1000);
        }

        // Clear the progress bar.
        statusBar.Progress(ref cookie, 0, "", 0, 0);
    }
    ```

3. 编译代码并开始调试。

4. 打开可视化工作室实验实例中的 **"工具**"菜单。 单击 **"调用测试状态栏命令"按钮**。

     您应该看到状态栏中的文本现在读取 **"写入进度"栏。** 您还应看到进度条每秒钟更新 20 秒。 之后，将清除状态栏和进度条。

### <a name="display-an-animation"></a>显示动画

1. 状态栏显示一个循环动画，指示长时间运行的操作（例如，在解决方案中生成多个项目）。 如果看不到此动画，请确保具有正确的**工具** > **选项**设置：

     转到 **"工具** > **选项** > **常规**"选项卡并取消选中**根据客户端性能自动调整视觉体验**。 然后检查子选项**启用丰富的客户端视觉体验**。 现在，在 Visual Studio 的实验实例中构建项目时，您应该能够看到动画。

     在此过程中，我们显示代表构建项目或解决方案的标准 Visual Studio 动画。

2. 打开*TestStatusBarCommand.cs*文件，`MenuItemCallback`并将该方法替换为以下代码：

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        IVsStatusbar statusBar =(IVsStatusbar)ServiceProvider.GetService(typeof(SVsStatusbar));

        // Use the standard Visual Studio icon for building.
        object icon = (short)Microsoft.VisualStudio.Shell.Interop.Constants.SBAI_Build;

        // Display the icon in the Animation region.
        statusBar.Animation(1, ref icon);

        // The message box pauses execution for you to look at the animation.
        System.Windows.Forms.MessageBox.Show("showing?");

        // Stop the animation.
        statusBar.Animation(0, ref icon);
    }
    ```

3. 编译代码并开始调试。

4. 打开可视化工作室实验实例中的 **"工具**"菜单，然后单击 **"调用测试状态栏命令**"。

     当您看到消息框时，还应在最右侧的状态栏中看到动画。 关闭消息框时，动画将消失。
