---
title: 创建和管理模式对话框 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- dialog boxes, managing in Visual Studio
ms.assetid: 491bc0de-7dba-478c-a76b-923440e090f3
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 29b0066f201fbb791d471d5cfb433d9a335aa775
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62431571"
---
# <a name="creating-and-managing-modal-dialog-boxes"></a>创建和管理模式对话框
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 Visual Studio 中创建模式对话框时，必须确保在对话框显示时已禁用对话框的父窗口，然后在关闭该对话框后重新启用父窗口。 如果不这样做，可能会收到错误： "Microsoft Visual Studio 无法关闭，因为模式对话框处于活动状态。 请关闭活动对话框，然后重试。 "  
  
 可以通过两种方式执行此操作。 如果你有一个 WPF 对话框，建议使用 <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow> ，然后调用来显示对话框，建议使用此方法 <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow.ShowModal%2A> 。 如果这样做，则无需管理父窗口的模式状态。  
  
 如果您的对话框不是 WPF，或出于某些其他原因而无法从派生您的对话框类 <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow> ，则您必须通过在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.GetDialogOwnerHwnd%2A> 显示对话框之前通过调用参数为 0 (false) 的方法来获取对话框的父级，然后在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.EnableModeless%2A> 关闭对话框并使用参数 1 (true) 再次调用方法。  
  
## <a name="creating-a-dialog-box-derived-from-dialogwindow"></a>创建从 DialogWindow 派生的对话框  
  
1. 创建名为 **OpenDialogTest** 的 VSIX 项目，并添加名为 **OpenDialog**的菜单命令。 有关如何执行此操作的详细信息，请参阅 [使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。  
  
2. 若要使用 <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow> 类，必须在 " **添加引用** " 对话框的 "框架" 选项卡中添加对以下程序集的引用 () ：  
  
    - PresentationCore  
  
    - PresentationFramework  
  
    - WindowsBase  
  
    - System.Xaml  
  
3. 在 OpenDialog.cs 中，添加以下 `using` 语句：  
  
    ```csharp  
    using Microsoft.VisualStudio.PlatformUI;  
    ```  
  
4. 声明一个名为 **TestDialogWindow** 的类，该类派生自 <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow> ：  
  
    ```csharp  
    class TestDialogWindow : DialogWindow  
    {. . .}  
    ```  
  
5. 若要最大程度地缩小对话框并最大化，请将 <xref:Microsoft.VisualStudio.PlatformUI.DialogWindowBase.HasMaximizeButton%2A> 和设置 <xref:Microsoft.VisualStudio.PlatformUI.DialogWindowBase.HasMinimizeButton%2A> 为 true：  
  
    ```csharp  
    internal TestDialogWindow()  
    {  
        this.HasMaximizeButton = true;  
        this.HasMinimizeButton = true;  
    }  
    ```  
  
6. 在 **OpenDialog. ShowMessageBox** 方法中，将现有代码替换为以下代码：  
  
    ```csharp  
    TestDialogWindow testDialog = new TestDialogWindow();  
    testDialog.ShowModal();  
    ```  
  
7. 生成并运行应用程序。 应显示 Visual Studio 的实验实例。 在实验实例的 " **工具** " 菜单中，应会看到名为 " **调用 OpenDialog**" 的命令。 单击此命令时，应会看到对话框窗口。 你应该能够最小化窗口并最大化。  
  
## <a name="creating-and-managing-a-dialog-box-not-derived-from-dialogwindow"></a>创建和管理不是从 DialogWindow 派生的对话框  
  
1. 对于此过程，可以使用在前面的过程中创建的 **OpenDialogTest** 解决方案，该解决方案具有相同的程序集引用。  
  
2. 添加以下 `using` 声明：  
  
    ```csharp  
    using System.Windows;  
    using Microsoft.Internal.VisualStudio.PlatformUI;  
    ```  
  
3. 创建一个名为 **TestDialogWindow2** 的类，该类派生自 <xref:System.Windows.Window> ：  
  
    ```csharp  
    class TestDialogWindow2 : Window  
    {. . .}  
    ```  
  
4. 添加对以下内容的私有引用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> ：  
  
    ```  
    private IVsUIShell shell;  
    ```  
  
5. 添加一个构造函数，该构造函数将引用设置为 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> ：  
  
    ```csharp  
    public TestDialogWindow2(IVsUIShell uiShell)  
    {  
        shell = uiShell;  
    }  
    ```  
  
6. 在 **OpenDialog. ShowMessageBox** 方法中，将现有代码替换为以下代码：  
  
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
  
7. 生成并运行应用程序。 在 " **工具** " 菜单中，应会看到名为 " **调用 OpenDialog**" 的命令。 单击此命令时，应会看到对话框窗口。
