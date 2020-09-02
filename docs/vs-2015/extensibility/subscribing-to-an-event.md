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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68160547"
---
# <a name="subscribing-to-an-event"></a>订阅事件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本演练介绍如何创建一个工具窗口，该窗口对运行的文档表中的事件进行响应 (RDT) 。 工具窗口承载实现的用户控件 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents> 。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.AdviseRunningDocTableEvents%2A>方法将接口连接到事件。  
  
## <a name="prerequisites"></a>必备条件  
 从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 你还可以在以后安装 VS SDK。 有关详细信息，请参阅 [安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。  
  
## <a name="subscribing-to-rdt-events"></a>订阅 RDT 事件  
  
#### <a name="to-create-an-extension-with-a-tool-window"></a>使用工具窗口创建扩展  
  
1. 使用 VSIX 模板创建名为 **RDTExplorer** 的项目，并添加一个名为 **RDTExplorerWindow**的自定义工具窗口项模板。  
  
     有关使用工具窗口创建扩展的详细信息，请参阅 [使用工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)。  
  
#### <a name="to-subscribe-to-rdt-events"></a>订阅 RDT 事件  
  
1. 打开 RDTExplorerWindowControl 文件并删除名为的按钮 `button1` 。 添加 <xref:System.Windows.Forms.ListBox> 控件并接受默认名称。 Grid 元素应如下所示：  
  
    ```xml  
    <Grid>  
        <StackPanel Orientation="Vertical" Margin="-10,10,10,0">  
            <TextBlock Margin="10" HorizontalAlignment="Center">RDTExplorerWindow</TextBlock>  
            <ListBox x:Name="listBox" Height="100" />  
        </StackPanel>  
    </Grid>  
    ```  
  
2. 在代码视图中打开 RDTExplorerWindow.cs 文件。 将以下 using 语句添加到文件的开头。  
  
    ```csharp  
    using Microsoft.VisualStudio;  
    using Microsoft.VisualStudio.Shell;  
    using Microsoft.VisualStudio.Shell.Interop;  
    ```  
  
3. 修改 `RDTExplorerWindow` 类，以便除了从类派生以外 <xref:Microsoft.VisualStudio.Shell.ToolWindowPane> ，还实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents> 接口。  
  
    ```csharp  
    public class RDTExplorerWindow : ToolWindowPane, IVsRunningDocTableEvents  
    {. . .}  
    ```  
  
4. 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents>。  
  
    - 实现接口。 将光标置于 IVsRunningDocTableEvents 名称上。 你应会在左边距中看到灯泡。 单击灯泡右侧的向下箭头，然后选择 " **实现接口**"。  
  
5. 在接口中的每个方法中，将行替换 `throw new NotImplementedException();` 为：  
  
    ```csharp  
    return VSConstants.S_OK;  
    ```  
  
6. 向 RDTExplorerWindow 类添加一个 cookie 字段。  
  
    ```csharp  
    private uint rdtCookie;   
    ```  
  
     这将保存方法返回的 cookie <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.AdviseRunningDocTableEvents%2A> 。  
  
7. 重写 RDTExplorerWindow 的 Initialize ( # A1 方法以注册 RDT 事件。 应始终在 ToolWindowPane 的 Initialize ( # A1 方法中获取服务，而不是在构造函数中获取。  
  
    ```csharp  
    protected override void Initialize()  
    {  
        IVsRunningDocumentTable rdt = (IVsRunningDocumentTable)  
        this.GetService(typeof(SVsRunningDocumentTable));  
        rdt.AdviseRunningDocTableEvents(this, out rdtCookie);  
    }  
    ```  
  
     <xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable>调用该服务以获取 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable> 接口。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.AdviseRunningDocTableEvents%2A>方法将 RDT 事件连接到实现的对象 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents> ，在本例中为 RDTExplorer 对象。  
  
8. 更新 RDTExplorerWindow 的 Dispose ( # A1 方法。  
  
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
  
     <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnadviseRunningDocTableEvents%2A>方法删除 `RDTExplorer` 和 RDT 事件通知之间的连接。  
  
9. 将以下行添加到处理程序的正文 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents.OnBeforeLastDocumentUnlock%2A> 中，就在 `return` 语句前面。  
  
    ```csharp  
    public int OnBeforeLastDocumentUnlock(uint docCookie, uint dwRDTLockType, uint dwReadLocksRemaining, uint dwEditLocksRemaining)  
    {  
        ((RDTExplorerWindowControl)this.Content).listBox.Items.Add("Entering OnBeforeLastDocumentUnlock");  
        return VSConstants.S_OK;  
    }  
    ```  
  
10. 将类似的行添加到 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocTableEvents.OnAfterFirstDocumentLock%2A> 处理程序的正文中，并添加到要在列表框中查看的其他事件。  
  
    ```csharp  
    public int OnAfterFirstDocumentLock(uint docCookie, uint dwRDTLockType, uint dwReadLocksRemaining, uint dwEditLocksRemaining)  
    {  
        ((RDTExplorerWindowControl)this.Content).listBox.Items.Add("Entering OnAfterFirstDocumentLock");  
        return VSConstants.S_OK;  
    }  
    ```  
  
11. 生成项目并启动调试。 出现 Visual Studio 实验实例。  
  
12. 打开 **RDTExplorerWindow** (**View/其他 Windows/RDTExplorerWindow**) 。  
  
     此时将打开 " **RDTExplorerWindow** " 窗口，其中包含一个空的事件列表。  
  
13. 打开或创建一个解决方案。  
  
     `OnBeforeLastDocument` `OnAfterFirstDocument` 触发事件时，事件列表中会出现每个事件的通知。
