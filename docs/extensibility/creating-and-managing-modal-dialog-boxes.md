---
title: 创建和管理模式对话框 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- dialog boxes, managing in Visual Studio
ms.assetid: 491bc0de-7dba-478c-a76b-923440e090f3
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 786a2fbe2b75c51420668eb1ab6f596213d3da9b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739492"
---
# <a name="create-and-manage-modal-dialog-boxes"></a>创建和管理模式对话框
在 Visual Studio 中创建模式对话框时，必须确保在显示对话框时禁用对话框的父窗口，然后在关闭对话框后重新启用父窗口。 如果不这样做，您可能会收到错误 *：Microsoft Visual Studio 无法关闭，因为模式对话框处于活动状态。关闭活动对话框，然后重试。*

有两种方法可以做到这一点。 如果具有 WPF 对话框，则建议的方法是从 派生<xref:Microsoft.VisualStudio.PlatformUI.DialogWindow>它，然后调用<xref:Microsoft.VisualStudio.PlatformUI.DialogWindow.ShowModal%2A>以显示对话框。 如果这样做，则不需要管理父窗口的模式状态。

如果对话框不是 WPF，或者由于其他原因无法从 派生<xref:Microsoft.VisualStudio.PlatformUI.DialogWindow>对话框类，则必须通过自己调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.GetDialogOwnerHwnd%2A>和管理模式状态来获取对话框的父级，方法是在显示对话框之前调用参数为 0（false）<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.EnableModeless%2A>的方法，并在关闭对话框后再次调用该方法，参数为 1（true）。

## <a name="create-a-dialog-box-derived-from-dialogwindow"></a>创建从对话框窗口派生的对话框

1. 创建名为**OpenDialogTest 的**VSIX 项目，并添加名为**OpenDialog**的菜单命令 。 有关如何执行此操作的详细信息，请参阅[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

2. 要使用<xref:Microsoft.VisualStudio.PlatformUI.DialogWindow>类，必须添加对以下程序集的引用（在 **"添加引用**"对话框的"框架"选项卡中）：

    - *PresentationCore*

    - *PresentationFramework*

    - *WindowsBase*

    - *System.Xaml*

3. 在*OpenDialog.cs*中，添加`using`以下语句：

    ```csharp
    using Microsoft.VisualStudio.PlatformUI;
    ```

4. 声明派生自<xref:Microsoft.VisualStudio.PlatformUI.DialogWindow>`TestDialogWindow`的命名类：

    ```csharp
    class TestDialogWindow : DialogWindow
    {. . .}
    ```

5. 为了能够最小化和最大化对话框，请设置<xref:Microsoft.VisualStudio.PlatformUI.DialogWindowBase.HasMaximizeButton%2A>和<xref:Microsoft.VisualStudio.PlatformUI.DialogWindowBase.HasMinimizeButton%2A>true：

    ```csharp
    internal TestDialogWindow()
    {
        this.HasMaximizeButton = true;
        this.HasMinimizeButton = true;
    }
    ```

6. 在`OpenDialog.ShowMessageBox`方法中，将现有代码替换为以下内容：

    ```csharp
    TestDialogWindow testDialog = new TestDialogWindow();
    testDialog.ShowModal();
    ```

7. 生成并运行应用程序。 应出现视觉工作室的实验实例。 在实验实例**的"工具"** 菜单上，您应该看到名为 **"调用 OpenDialog"** 的命令。 单击此命令时，应看到对话框窗口。 您应该能够最小化和最大化窗口。

## <a name="create-and-manage-a-dialog-box-not-derived-from-dialogwindow"></a>创建和管理未从对话框窗口派生的对话框

1. 对于此过程，可以使用在上一过程中创建的**OpenDialogTest**解决方案，并使用相同的程序集引用。

2. 添加以下`using`声明：

    ```csharp
    using System.Windows;
    using Microsoft.Internal.VisualStudio.PlatformUI;
    ```

3. 创建名为`TestDialogWindow2`的类，该类派生<xref:System.Windows.Window>自 ：

    ```csharp
    class TestDialogWindow2 : Window
    {. . .}
    ```

4. 向 添加对<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell>的私有引用。

    ```
    private IVsUIShell shell;
    ```

5. 添加将引用设置为<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell>的构造函数。

    ```csharp
    public TestDialogWindow2(IVsUIShell uiShell)
    {
        shell = uiShell;
    }
    ```

6. 在`OpenDialog.ShowMessageBox`方法中，将现有代码替换为以下内容：

    ```csharp
    IVsUIShell uiShell = (IVsUIShell)ServiceProvider.GetService(typeof(SVsUIShell));

    TestDialogWindow2 testDialog2 = new TestDialogWindow2(uiShell);
    //get the owner of this dialog
    IntPtr hwnd;
    uiShell.GetDialogOwnerHwnd(out hwnd);
    testDialog2.WindowStartupLocation = System.Windows.WindowStartupLocation.CenterOwner;
    uiShell.EnableModeless(0);
    try
    {
        WindowHelper.ShowModal(testDialog2, hwnd);
    }
    finally
    {
        // This will take place after the window is closed.
        uiShell.EnableModeless(1);
    }
    ```

7. 生成并运行应用程序。 在 **"工具"** 菜单上，您应该看到名为 **"调用打开对话**"的命令。 单击此命令时，应看到对话框窗口。
