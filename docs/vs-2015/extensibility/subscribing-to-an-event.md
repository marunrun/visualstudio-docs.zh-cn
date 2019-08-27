---
title: 订阅事件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- running document table (RDT), responding to events
- running document table (RDT), subscribing to events
ms.assetid: e94a4fea-94df-488e-8560-9538413422bc
caps.latest.revision: 36
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 324e74c78f01da47c544b5f640ad0bd9052a1bb4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68160547"
---
# <a name="subscribing-to-an-event"></a>订阅事件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此演练说明了如何创建一个工具窗口，运行文档表 (RDT) 中的事件做出响应。 工具窗口承载实现的用户控件<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents>。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.AdviseRunningDocTableEvents%2A>方法连接到事件接口。  
  
## <a name="prerequisites"></a>系统必备  
 从 Visual Studio 2015 开始，您并不安装 Visual Studio SDK 从下载中心获得。 它是作为 Visual Studio 安装程序中的可选功能包含在内。 此外可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。  
  
## <a name="subscribing-to-rdt-events"></a>订阅 RDT 事件  
  
#### <a name="to-create-an-extension-with-a-tool-window"></a>若要使用的工具窗口创建扩展  
  
1. 创建一个名为项目**RDTExplorer**使用 VSIX 模板，并添加一个名为的自定义工具窗口项模板**RDTExplorerWindow**。  
  
     有关使用工具窗口创建扩展的详细信息，请参阅[与工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)。  
  
#### <a name="to-subscribe-to-rdt-events"></a>若要订阅 RDT 事件  
  
1. 打开 RDTExplorerWindowControl.xaml 文件，并删除名为的按钮`button1`。 添加<xref:System.Windows.Forms.ListBox>控制并接受默认名称。 网格元素应如下所示：  
  
    ```xml  
    <Grid>  
        <StackPanel Orientation="Vertical" Margin="-10,10,10,0">  
            <TextBlock Margin="10" HorizontalAlignment="Center">RDTExplorerWindow</TextBlock>  
            <ListBox x:Name="listBox" Height="100" />  
        </StackPanel>  
    </Grid>  
    ```  
  
2. 在代码视图中打开 RDTExplorerWindow.cs 文件。 将以下代码添加到起始位置的文件的 using 语句。  
  
    ```csharp  
    using Microsoft.VisualStudio;  
    using Microsoft.VisualStudio.Shell;  
    using Microsoft.VisualStudio.Shell.Interop;  
    ```  
  
3. 修改`RDTExplorerWindow`类这样的除了派生自<xref:Microsoft.VisualStudio.Shell.ToolWindowPane>类，它实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents>接口。  
  
    ```csharp  
    public class RDTExplorerWindow : ToolWindowPane, IVsRunningDocTableEvents  
    {. . .}  
    ```  
  
4. 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents>。  
  
    - 实现接口。 将光标置于 IVsRunningDocTableEvents 名称。 应会看到灯泡在左边距中。 单击灯泡图标右侧的向下箭头，然后选择**实现接口**。  
  
5. 在接口中每个方法，将为行`throw new NotImplementedException();`与此：  
  
    ```csharp  
    return VSConstants.S_OK;  
    ```  
  
6. 将 cookie 字段添加到 RDTExplorerWindow 类。  
  
    ```csharp  
    private uint rdtCookie;   
    ```  
  
     它将保存返回的 cookie<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.AdviseRunningDocTableEvents%2A>方法。  
  
7. 重写 RDTExplorerWindow 的 initialize （） 方法以注册 RDT 事件。 始终应在 ToolWindowPane 的 initialize （） 方法中，在构造函数中不显示服务。  
  
    ```csharp  
    protected override void Initialize()  
    {  
        IVsRunningDocumentTable rdt = (IVsRunningDocumentTable)  
        this.GetService(typeof(SVsRunningDocumentTable));  
        rdt.AdviseRunningDocTableEvents(this, out rdtCookie);  
    }  
    ```  
  
     <xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable>服务调用以获得<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable>接口。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.AdviseRunningDocTableEvents%2A>方法连接到一个对象，实现 RDT 事件<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents>，在这种情况下，RDTExplorer 对象。  
  
8. 更新 RDTExplorerWindow 的 dispose （） 方法。  
  
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
  
     <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnadviseRunningDocTableEvents%2A>方法删除之间的连接`RDTExplorer`和 RDT 事件通知。  
  
9. 将以下行添加到正文<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents.OnBeforeLastDocumentUnlock%2A>处理程序，再`return`语句。  
  
    ```csharp  
    public int OnBeforeLastDocumentUnlock(uint docCookie, uint dwRDTLockType, uint dwReadLocksRemaining, uint dwEditLocksRemaining)  
    {  
        ((RDTExplorerWindowControl)this.Content).listBox.Items.Add("Entering OnBeforeLastDocumentUnlock");  
        return VSConstants.S_OK;  
    }  
    ```  
  
10. 将类似的代码行添加到正文<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents.OnAfterFirstDocumentLock%2A>处理程序和其他你想要在列表框中看到的事件。  
  
    ```csharp  
    public int OnAfterFirstDocumentLock(uint docCookie, uint dwRDTLockType, uint dwReadLocksRemaining, uint dwEditLocksRemaining)  
    {  
        ((RDTExplorerWindowControl)this.Content).listBox.Items.Add("Entering OnAfterFirstDocumentLock");  
        return VSConstants.S_OK;  
    }  
    ```  
  
11. 生成项目并启动调试。 将显示 Visual Studio 实验实例。  
  
12. 打开**RDTExplorerWindow** (**视图 / 其他 Windows / RDTExplorerWindow**)。  
  
     **RDTExplorerWindow**窗口打开时的空的事件列表。  
  
13. 打开或创建一个解决方案。  
  
     作为`OnBeforeLastDocument`和`OnAfterFirstDocument`的事件触发，每个事件的通知会显示在事件列表。
