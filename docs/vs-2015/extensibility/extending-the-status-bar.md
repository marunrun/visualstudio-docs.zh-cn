---
title: 扩展状态栏 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- status bars, about status bars
- status bars, overview
ms.assetid: f955115c-4c5f-45ec-b41b-365868c5ec0c
caps.latest.revision: 24
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 28fc1155279ec624cea576b5a70a25800d4ff837
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204408"
---
# <a name="extending-the-status-bar"></a>扩展状态栏
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以使用 IDE 底部的 Visual Studio 状态栏显示信息。  
  
 扩展状态栏时，可以在四个区域中显示信息和 UI：反馈区域、进度栏、动画区域和设计器区域。 反馈区域允许您显示文本并突出显示文本。 进度栏显示短时间运行的操作（例如保存文件）的增量进度。 动画区域为长时间运行的操作或不确定长度的操作（如在解决方案中生成多个项目）显示连续循环的动画。 设计器区域显示光标位置的行号和列号。  
  
 您可以使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbar> 服务) 中的接口 (来获取状态栏 <xref:Microsoft.VisualStudio.Shell.Interop.SVsStatusbar> 。 此外，位于窗口框架上的任何对象都可以通过实现接口来注册为状态栏客户端对象 <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser> 。 每当激活窗口时，Visual Studio 就会在该窗口中查询该接口的对象 `IVsStatusbarUser` 。 如果找到，它将 <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser.SetInfo%2A> 在返回的接口上调用方法，并且对象可从该方法中更新状态栏。 例如，文档窗口可以使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser.SetInfo%2A> 方法在设计器区域处于活动状态时更新其信息。  
  
 以下过程假定你了解如何创建 VSIX 项目并添加自定义菜单命令。 有关信息，请参阅 [使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。  
  
## <a name="modifying-the-status-bar"></a>修改状态栏  
 此过程演示如何设置和获取文本、显示静态文本，以及在状态栏的反馈区域中突出显示所显示的文本。  
  
#### <a name="reading-and-writing-to-the-status-bar"></a>读取和写入状态栏  
  
1. 创建名为 **TestStatusBarExtension** 的 VSIX 项目，并添加名为 **TestStatusBarCommand**的菜单命令。  
  
2. 在 TestStatusBarCommand.cs 中，将命令处理程序方法代码 (MenuItemCallback) 替换为以下代码：  
  
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
  
4. 在 Visual Studio 的实验实例中打开 " **工具** " 菜单。 单击 " **调用 TestStatusBarCommand** " 按钮。  
  
     应该会看到，状态栏中的文本现在显示 **"我们刚刚写入状态栏"。** 并且显示的消息框具有相同的文本。  
  
#### <a name="updating-the-progress-bar"></a>更新进度栏  
  
1. 在此过程中，我们将演示如何初始化和更新进度栏。  
  
2. 打开 TestStatusBarCommand.cs 文件并将 MenuItemCallback 方法替换为以下代码：  
  
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
  
4. 在 Visual Studio 的实验实例中打开 " **工具** " 菜单。 单击 " **调用 TestStatusBarCommand** " 按钮。  
  
     应会看到，状态栏中的文本现在会显示 **"写入进度栏"。** 还应看到进度栏每秒更新一次的时间为20秒。 之后，会清除状态栏和进度栏。  
  
#### <a name="displaying-an-animation"></a>显示动画  
  
1. 状态栏显示循环动画，该动画指示长时间运行的操作 (例如，在解决方案) 中生成多个项目。 如果看不到此动画，请确保具有正确的 " **工具/选项** " 设置：  
  
     中转到 " **工具"/"选项"/"常规** " 选项卡，取消选中 " **基于客户端性能自动调整视觉体验"**。 然后选中 " **启用丰富的客户端视觉体验**" 子选项。 在 Visual Studio 的实验实例中生成项目时，现在应能够看到动画。  
  
     在此过程中，我们将显示表示生成项目或解决方案的标准 Visual Studio 动画。  
  
2. 打开 TestStatusBarCommand.cs 文件并将 MenuItemCallback 方法替换为以下代码：  
  
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
  
4. 在 Visual Studio 的实验实例中打开 " **工具** " 菜单，然后单击 " **调用 TestStatusBarCommand**"。  
  
     看到消息框时，还应在最右侧的状态栏中看到动画。 关闭该消息框后，动画将会消失。
