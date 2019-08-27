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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62431571"
---
# <a name="creating-and-managing-modal-dialog-boxes"></a>创建和管理模式对话框
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在创建模式对话框在 Visual Studio 中的，必须确保父窗口的对话框的已禁用时显示的对话框，然后在对话框关闭后重新启用父窗口。 如果不这样做，可能会收到错误："Microsoft Visual Studio 不能关闭，因为模式对话框处于活动状态。 关闭活动对话框，然后重试。"  
  
 有两种方法执行此操作。 建议的方法，WPF 对话框中，如果是从它派生<xref:Microsoft.VisualStudio.PlatformUI.DialogWindow>，然后调用<xref:Microsoft.VisualStudio.PlatformUI.DialogWindow.ShowModal%2A>以显示对话框。 如果这样做，您不需要管理模式的父窗口的状态。  
  
 如果您的对话框不是 WPF 中，或某些其他原因不能派生对话框类从<xref:Microsoft.VisualStudio.PlatformUI.DialogWindow>，则必须通过调用获取对话框的父<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.GetDialogOwnerHwnd%2A>和你自己，通过调用管理模式状态<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.EnableModeless%2A>方法参数为 0 (false) 之前显示的对话框和关闭该对话框之后调用该方法使用的参数 1 (true)。  
  
## <a name="creating-a-dialog-box-derived-from-dialogwindow"></a>创建对话框派生自 DialogWindow  
  
1. 创建一个名为的 VSIX 项目**OpenDialogTest**并添加名为的菜单命令**OpenDialog**。 有关如何执行此操作的详细信息，请参阅[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。  
  
2. 若要使用<xref:Microsoft.VisualStudio.PlatformUI.DialogWindow>类，必须添加对以下程序集的引用 (在的框架选项卡**添加引用**对话框):  
  
    - PresentationCore  
  
    - PresentationFramework  
  
    - WindowsBase  
  
    - System.Xaml  
  
3. 在 OpenDialog.cs，添加以下`using`语句：  
  
    ```csharp  
    using Microsoft.VisualStudio.PlatformUI;  
    ```  
  
4. 声明一个名为的类**TestDialogWindow**派生<xref:Microsoft.VisualStudio.PlatformUI.DialogWindow>:  
  
    ```csharp  
    class TestDialogWindow : DialogWindow  
    {. . .}  
    ```  
  
5. 若要能够最小化和最大化对话框中，设置<xref:Microsoft.VisualStudio.PlatformUI.DialogWindowBase.HasMaximizeButton%2A>和<xref:Microsoft.VisualStudio.PlatformUI.DialogWindowBase.HasMinimizeButton%2A>为 true:  
  
    ```csharp  
    internal TestDialogWindow()  
    {  
        this.HasMaximizeButton = true;  
        this.HasMinimizeButton = true;  
    }  
    ```  
  
6. 在中**OpenDialog.ShowMessageBox**方法中，现有代码替换为以下：  
  
    ```csharp  
    TestDialogWindow testDialog = new TestDialogWindow();  
    testDialog.ShowModal();  
    ```  
  
7. 生成并运行应用程序。 应显示 Visual Studio 的实验实例。 上**工具**看到名为的命令菜单中的实验实例**调用 OpenDialog**。 当单击此命令时，你应看到对话框窗口。 您应能够最小化和最大化窗口。  
  
## <a name="creating-and-managing-a-dialog-box-not-derived-from-dialogwindow"></a>创建和管理从 DialogWindow 不派生的对话框  
  
1. 对于此过程中，你可以使用**OpenDialogTest**具有相同的程序集引用的上一个过程中创建的解决方案。  
  
2. 以下代码添加到`using`声明：  
  
    ```csharp  
    using System.Windows;  
    using Microsoft.Internal.VisualStudio.PlatformUI;  
    ```  
  
3. 创建一个名为类**TestDialogWindow2**派生<xref:System.Windows.Window>:  
  
    ```csharp  
    class TestDialogWindow2 : Window  
    {. . .}  
    ```  
  
4. 添加对私有引用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell>:  
  
    ```  
    private IVsUIShell shell;  
    ```  
  
5. 添加到设置的引用的构造函数<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell>:  
  
    ```csharp  
    public TestDialogWindow2(IVsUIShell uiShell)  
    {  
        shell = uiShell;  
    }  
    ```  
  
6. 在中**OpenDialog.ShowMessageBox**方法中，现有代码替换为以下：  
  
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
  
7. 生成并运行应用程序。 上**工具**看到名为的命令菜单**调用 OpenDialog**。 当单击此命令时，你应看到对话框窗口。
