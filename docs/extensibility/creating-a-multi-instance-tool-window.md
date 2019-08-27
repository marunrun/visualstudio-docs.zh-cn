---
title: 创建多实例工具窗口 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- multi
- tool windows
ms.assetid: 4a7872f1-acc9-4f43-8932-5a526b36adea
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a9c31f1c439db69b3795d789758b0604a539ef81
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66341630"
---
# <a name="create-a-multi-instance-tool-window"></a>创建多实例工具窗口
您可以编程的工具窗口，以便它的多个实例可以同时打开。 默认情况下，工具窗口可以打开的仅一个实例。

当使用多实例工具窗口时，可以显示多个相关的源的信息，请参阅在同一时间。 例如，您可以将多行<xref:System.Windows.Forms.TextBox>控件的多实例工具窗口中，以便多个代码段编程会话期间可同时提供。 此外，例如，你可能会使<xref:System.Windows.Forms.DataGrid>控件和下拉列表框中的多实例工具窗口，以便可以同时跟踪多个实时数据源。

## <a name="create-a-basic-single-instance-tool-window"></a>创建基本 （单实例） 的工具窗口

1. 创建一个名为项目**MultiInstanceToolWindow**使用 VSIX 模板，并添加一个名为的自定义工具窗口项模板**MIToolWindow**。

    > [!NOTE]
    > 有关使用工具窗口创建扩展的详细信息，请参阅[与工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)。

## <a name="make-a-tool-window-multi-instance"></a>使工具窗口的多实例

1. 打开*MIToolWindowPackage.cs*文件并查找`ProvideToolWindow`属性。 和`MultiInstances=true`参数，如下面的示例中所示：

    ```csharp
    [PackageRegistration(UseManagedResourcesOnly = true)]
        [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)] // Info on this package for Help/About
        [ProvideMenuResource("Menus.ctmenu", 1)]
        [ProvideToolWindow(typeof(MultiInstanceToolWindow.MIToolWindow), MultiInstances = true)]
        [Guid(MIToolWindowPackage.PackageGuidString)]
        public sealed class MIToolWindowPackage : Package
    {. . .}
    ```

2. 在中*MIToolWindowCommand.cs*文件中，找到`ShowToolWindos()`方法。 在此方法中，调用<xref:Microsoft.VisualStudio.Shell.Package.FindToolWindow%2A>方法，设置其`create`标记，用于`false`，以便它将循环访问现有的工具窗口实例之前是可用`id`找到。

3. 若要创建工具窗口实例，调用<xref:Microsoft.VisualStudio.Shell.Package.FindToolWindow%2A>方法，设置其`id`为可用的值并将其`create`标记，用于`true`。

    默认情况下的值`id`的参数<xref:Microsoft.VisualStudio.Shell.Package.FindToolWindow%2A>方法是`0`。 此值可以是单实例工具窗口。 对于要托管的多个实例，每个实例必须具有自己的唯一`id`。

4. 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A>方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame>返回的对象<xref:Microsoft.VisualStudio.Shell.ToolWindowPane.Frame%2A>工具窗口实例的属性。

5. 默认情况下，`ShowToolWindow`方法创建的工具窗口项模板创建单实例工具窗口。 下面的示例演示如何修改`ShowToolWindow`方法来创建多个实例。

    ```csharp
    private void ShowToolWindow(object sender, EventArgs e)
    {
        for (int i = 0; i < 10; i++)
        {
            ToolWindowPane window = this.package.FindToolWindow(typeof(MIToolWindow), i, false);
            if (window == null)
            {
                // Create the window with the first free ID.
                window = (ToolWindowPane)this.package.FindToolWindow(typeof(MIToolWindow), i, true);
                if ((null == window) || (null == window.Frame))
                {
                    throw new NotSupportedException("Cannot create tool window");
                }

            IVsWindowFrame windowFrame = (IVsWindowFrame)window.Frame;
            Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure(windowFrame.Show());
            break;
            }
        }
    }
    ```
