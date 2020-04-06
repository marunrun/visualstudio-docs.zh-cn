---
title: 订阅事件 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- running document table (RDT), responding to events
- running document table (RDT), subscribing to events
ms.assetid: e94a4fea-94df-488e-8560-9538413422bc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6aefe2efce897aefc26f63835844b0cc705fb5b1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699689"
---
# <a name="subscribing-to-an-event"></a>订阅事件
本演练介绍如何创建响应正在运行的文档表 （RDT） 中的事件的工具窗口。 工具窗口承载实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents>的用户控件。 该方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.AdviseRunningDocTableEvents%2A>将接口连接到事件。

## <a name="prerequisites"></a>先决条件
 从 Visual Studio 2015 开始，您不会从下载中心安装 Visual Studio SDK。 它作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="subscribing-to-rdt-events"></a>订阅 RDT 事件

#### <a name="to-create-an-extension-with-a-tool-window"></a>使用工具窗口创建扩展

1. 使用 VSIX 模板创建名为**RDTExplorer**的项目，并添加名为**RDTExplorerWindow**的自定义工具窗口项模板。

     有关使用工具窗口创建扩展的详细信息，请参阅[使用工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)。

#### <a name="to-subscribe-to-rdt-events"></a>订阅 RDT 事件

1. 打开 RDTExplorerWindowControl.xaml 文件并删除名为`button1`的按钮。 添加<xref:System.Windows.Forms.ListBox>控件并接受默认名称。 网格元素应如下所示：

    ```xml
    <Grid>
        <StackPanel Orientation="Vertical" Margin="-10,10,10,0">
            <TextBlock Margin="10" HorizontalAlignment="Center">RDTExplorerWindow</TextBlock>
            <ListBox x:Name="listBox" Height="100" />
        </StackPanel>
    </Grid>
    ```

2. 在代码视图中打开RDTExplorerWindow.cs文件。 将以下使用指令添加到文件的开头。

    ```csharp
    using Microsoft.VisualStudio;
    using Microsoft.VisualStudio.Shell;
    using Microsoft.VisualStudio.Shell.Interop;
    ```

3. 修改类`RDTExplorerWindow`，以便除了从<xref:Microsoft.VisualStudio.Shell.ToolWindowPane>类派生外，它还实现了<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents>接口。

    ```csharp
    public class RDTExplorerWindow : ToolWindowPane, IVsRunningDocTableEvents
    {. . .}
    ```

4. 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents>。

    - 实现接口。 将光标放在 IV 运行文档表事件名称上。 你应该在左边边看到一个灯泡。 单击灯泡右侧的向下箭头，然后选择 **"实现"界面**。

5. 在接口中的每个方法中，将行`throw new NotImplementedException();`替换为：

    ```csharp
    return VSConstants.S_OK;
    ```

6. 将 Cookie 字段添加到 RDTExplorerWindow 类。

    ```csharp
    private uint rdtCookie;
    ```

     这将保存方法返回的<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.AdviseRunningDocTableEvents%2A>Cookie。

7. 重写 RDTExplorerWindow 的初始化（） 方法以注册 RDT 事件。 应始终在 ToolWindowPane 的初始化（） 方法中获取服务，而不是在构造函数中获取服务。

    ```csharp
    protected override void Initialize()
    {
        IVsRunningDocumentTable rdt = (IVsRunningDocumentTable)
        this.GetService(typeof(SVsRunningDocumentTable));
        rdt.AdviseRunningDocTableEvents(this, out rdtCookie);
    }
    ```

     调用<xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable>该服务以获取<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable>接口。 该方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.AdviseRunningDocTableEvents%2A>将 RDT 事件连接到实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents>RDTExplorer 对象的对象。

8. 更新 RDTExplorerWindow 的 Dispose（） 方法。

    ```csharp
    protected override void Dispose(bool disposing)
    {
        // Release the RDT cookie.
        IVsRunningDocumentTable rdt = (IVsRunningDocumentTable)
            Package.GetGlobalService(typeof(SVsRunningDocumentTable));
        rdt.UnadviseRunningDocTableEvents(rdtCookie);

        base.Dispose(disposing);
    }
    ```

     该方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnadviseRunningDocTableEvents%2A>删除和 RDT`RDTExplorer`事件通知之间的连接。

9. 将以下行添加到处理程序的<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents.OnBeforeLastDocumentUnlock%2A>正文中，就在`return`语句之前。

    ```csharp
    public int OnBeforeLastDocumentUnlock(uint docCookie, uint dwRDTLockType, uint dwReadLocksRemaining, uint dwEditLocksRemaining)
    {
        ((RDTExplorerWindowControl)this.Content).listBox.Items.Add("Entering OnBeforeLastDocumentUnlock");
        return VSConstants.S_OK;
    }
    ```

10. 向<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents.OnAfterFirstDocumentLock%2A>处理程序的正文和要在列表框中看到的其他事件添加类似的行。

    ```csharp
    public int OnAfterFirstDocumentLock(uint docCookie, uint dwRDTLockType, uint dwReadLocksRemaining, uint dwEditLocksRemaining)
    {
        ((RDTExplorerWindowControl)this.Content).listBox.Items.Add("Entering OnAfterFirstDocumentLock");
        return VSConstants.S_OK;
    }
    ```

11. 生成项目并启动调试。 将显示可视化工作室实验实例。

12. 打开**RDTExplorer 窗口**（**视图 / 其他窗口 / RDTExplorer 窗口**）。

     **RDTExplorer 窗口**窗口打开时，将打开一个空事件列表。

13. 打开或创建解决方案。

     触发`OnBeforeLastDocument`事件`OnAfterFirstDocument`时，事件列表中将显示每个事件的通知。
