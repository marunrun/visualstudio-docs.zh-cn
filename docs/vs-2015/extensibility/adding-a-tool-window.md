---
title: 添加工具窗口 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- tutorials
- tool windows
ms.assetid: 8e16c381-03c8-404e-92ef-3614cdf3150a
caps.latest.revision: 53
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9099bc79a555f908ddda12dc9da83f015791fd86
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63444834"
---
# <a name="adding-a-tool-window"></a>添加工具窗口
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在本演练中你将了解如何创建工具窗口并将其集成到 Visual Studio 中，按以下方式：  
  
- 将控件添加到工具窗口。  
  
- 将工具栏添加到工具窗口。  
  
- 将命令添加到工具栏。  
  
- 实现命令。  
  
- 设置工具窗口的默认位置。  
  
## <a name="prerequisites"></a>系统必备  
 从 Visual Studio 2015 开始，您并不安装 Visual Studio SDK 从下载中心获得。 它是作为 Visual Studio 安装程序中的可选功能包含在内。 此外可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。  
  
## <a name="creating-a-tool-window"></a>创建工具窗口  
  
1. 创建一个名为项目**FirstToolWin**使用 VSIX 模板，并添加一个名为的自定义工具窗口项模板**FirstToolWindow**。  
  
    > [!NOTE]
    > 有关使用工具窗口创建扩展的详细信息，请参阅[与工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)。  
  
## <a name="add-a-control-to-the-tool-window"></a>将控件添加到工具窗口  
  
1. 删除默认的控制。 打开 FirstToolWindowControl.xaml 并删除**单击我 ！** 按钮。  
  
2. 在中**工具箱**，展开**所有 WPF 控件**部分并将其拖**媒体元素**控制对**FirstToolWindowControl**窗体。 选择控件，然后在**属性**窗口中，命名此元素**mediaElement1**。  
  
## <a name="add-a-toolbar-to-the-tool-window"></a>将工具栏添加到工具窗口  
 通过按以下方式添加工具栏，可以确保其渐变样式和颜色是与 IDE 的其余部分保持一致。  
  
1. 在中**解决方案资源管理器**，打开 FirstToolWindowPackage.vsct。 .Vsct 文件使用 XML 工具窗口中定义的图形用户界面 (GUI) 元素。  
  
2. 在中`<Symbols>`部分中，找到`<GuidSymbol>`节点其`name`属性是`guidFirstToolWindowPackageCmdSet`。 添加以下两个`<IDSymbol>`元素的列表与`<IDSymbol>`此节点可以定义一个工具栏和工具栏组中的元素。  
  
    ```xml  
    <IDSymbol name="ToolbarID" value="0x1000" />  
    <IDSymbol name="ToolbarGroupID" value="0x1001" />  
    ```  
  
3. 正上方`<Buttons>`部分中，创建`<Menus>`类似于下面这样的部分：  
  
    ```xml  
    <Menus>  
        <Menu guid="guidFirstToolWindowPackageCmdSet" id="ToolbarID" priority="0x0000" type="ToolWindowToolbar">  
            <Parent guid="guidFirstToolWindowPackageCmdSet" id="ToolbarID" />  
            <Strings>  
                <ButtonText>Tool Window Toolbar</ButtonText>  
                <CommandName>Tool Window Toolbar</CommandName>  
            </Strings>  
        </Menu>  
    </Menus>  
    ```  
  
     有几种不同的菜单。 此菜单是一个由定义的工具栏中的工具窗口中，其`type`属性。 `guid`和`id`设置构成了工具栏的完全限定的 ID。 通常情况下，`<Parent>`菜单的是包含的组。 但是，作为其自己的父定义一个工具栏。 因此，用于相同的标识符`<Menu>`和`<Parent>`元素。 `priority`属性为只是"0。  
  
4. 工具栏类似于在很多方面的菜单。 例如，就像一个菜单可能具有的命令组，工具栏也可能有组。 （在菜单上的命令组分隔水平线条。 在工具栏上未分隔成组可视分隔线。）  
  
     添加`<Groups>`节，其中包含`<Group>`元素。 这将定义组中声明其 ID`<Symbols>`部分。 添加`<Groups>`紧后面部分`<Menus>`部分。  
  
    ```xml  
    <Groups>  
       <Group guid="guidFirstToolWindowPackageCmdSet" id="ToolbarGroupID" priority="0x0000">  
           <Parent guid="guidFirstToolWindowPackageCmdSet" id="ToolbarID" />  
       </Group>  
    </Groups>  
    ```  
  
     通过将父 GUID 和 ID 设置为 GUID 和 ID 的工具栏，您可以将组添加到工具栏。  
  
## <a name="add-a-command-to-the-toolbar"></a>将命令添加到工具栏  
 将命令添加到工具栏上，将显示为一个按钮。  
  
1. 在`<Symbols>`部分中，组声明的工具栏和工具栏后，只需声明以下 IDSymbol 元素。  
  
    ```xml  
    <IDSymbol name="cmdidWindowsMedia" value="0x0100" />  
    <IDSymbol name="cmdidWindowsMediaOpen" value="0x132" />  
    ```  
  
2. 将按钮元素内的添加`<Buttons>`部分。 此元素将显示在工具窗口中，使用搜索 （放大镜） 图标的工具栏上。  
  
    ```xml  
    <Button guid="guidFirstToolWindowPackageCmdSet" id="cmdidWindowsMediaOpen" priority="0x0101" type="Button">  
        <Parent guid="guidFirstToolWindowPackageCmdSet" id="ToolbarGroupID"/>  
        <Icon guid="guidImages" id="bmpPicSearch" />  
        <Strings>  
            <CommandName>cmdidWindowsMediaOpen</CommandName>  
            <ButtonText>Load File</ButtonText>  
        </Strings>  
    </Button>  
    ```  
  
3. 打开 FirstToolWindowCommand.cs 和之后的现有字段的类中添加以下行。  
  
    ```csharp  
    public const string guidFirstToolWindowPackageCmdSet = "00000000-0000-0000-0000-0000";  // get the GUID from the .vsct file  
    public const uint cmdidWindowsMedia =        0x100;   
    public const int cmdidWindowsMediaOpen = 0x132;  
    public const int ToolbarID = 0x1000;  
    ```  
  
     执行此操作使你的命令可在代码中。  
  
## <a name="add-a-mediaplayer-property-to-firsttoolwindowcontrol"></a>将 MediaPlayer 属性添加到 FirstToolWindowControl  
 从工具栏控件的事件处理程序，你的代码必须能够访问媒体播放器控件，它是 FirstToolWindowControl 类的子级。  
  
 在中**解决方案资源管理器**，右键单击 FirstToolWindowControl.xaml，单击**查看代码**，并将以下代码添加到 FirstToolWindowControl 类。  
  
```csharp  
public System.Windows.Controls.MediaElement MediaPlayer  
{  
    get { return mediaElement1; }  
}  
```  
  
## <a name="instantiate-the-tool-window-and-toolbar"></a>实例化的工具窗口和工具栏  
 添加一个工具栏和菜单命令调用**打开的文件**对话框，并在播放所选的媒体文件。  
  
1. 打开 FirstToolWindow.cs 并添加以下`using`语句。  
  
    ```csharp  
    using System.ComponentModel.Design;  
    using System.Windows.Forms;  
    using Microsoft.VisualStudio.Shell.Interop;   
    ```  
  
2. 在 FirstToolWindow 类中，添加对 FirstToolWindowControl 控件的公共引用。  
  
    ```csharp  
    public FirstToolWindowControl control;  
    ```  
  
3. 构造函数末尾，将此控件变量设置的新创建的控件。  
  
    ```csharp  
    control = new FirstToolWindowControl();   
    base.Content = control;  
    ```  
  
4. 实例化构造函数中的工具栏。  
  
    ```csharp  
    this.ToolBar = new CommandID(new Guid(FirstToolWindowCommand.guidFirstToolWindowPackageCmdSet),   
        FirstToolWindowCommand.ToolbarID);  
    this.ToolBarLocation = (int)VSTWT_LOCATION.VSTWT_TOP;  
    ```  
  
5. 此时 FirstToolWindow 构造函数应如下所示：  
  
    ```csharp  
    public FirstToolWindow() : base(null)  
    {  
        this.Caption = "FirstToolWindow";  
        this.BitmapResourceID = 301;  
        this.BitmapIndex = 1;  
        control = new FirstToolWindowControl();  
        base.Content = control;  
        this.ToolBar = new CommandID(new Guid(FirstToolWindowCommand.guidFirstToolWindowPackageCmdSet),   
            FirstToolWindowCommand.ToolbarID);  
            this.ToolBarLocation = (int)VSTWT_LOCATION.VSTWT_TOP;  
    }  
    ```  
  
6. 将菜单命令添加到工具栏。 在 FirstToolWindowCommand.cs 类中，添加以下 using 语句  
  
    ```csharp  
    using System.Windows.Forms;  
    ```  
  
7. 在 FirstToolWindowCommand 类中，ShowToolWindow() 方法末尾添加以下代码。 将在下一节中实现按钮处理程序命令。  
  
    ```csharp  
    // Create the handles for the toolbar command.   
    var mcs = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;  
    var toolbarbtnCmdID = new CommandID(new Guid(FirstToolWindowCommand.guidFirstToolWindowPackageCmdSet),  
        FirstToolWindowCommand.cmdidWindowsMediaOpen);  
    var menuItem = new MenuCommand(new EventHandler(  
        ButtonHandler), toolbarbtnCmdID);  
    mcs.AddCommand(menuItem);  
    ```  
  
#### <a name="to-implement-a-menu-command-in-the-tool-window"></a>在工具窗口中实现菜单命令  
  
1. 在 FirstToolWindowCommand 类中，添加按钮处理程序调用的方法，**打开的文件**对话框。 在已选定一个文件，它会播放媒体文件。  
  
2. 在 FirstToolWindowCommand 类中，将添加到 FirstToolWindow 窗口 FindToolWindow() 方法中创建的私有引用。  
  
    ```csharp  
    private FirstToolWindow window;  
    ```  
  
3. 更改设置，以便按钮处理程序命令处理程序可以访问窗口控件上面定义窗口 ShowToolWindow() 方法。 下面是完整的 ShowToolWindow() 方法。  
  
    ```csharp  
    private void ShowToolWindow(object sender, EventArgs e)  
    {  
        window = (FirstToolWindow) this.package.FindToolWindow(typeof(FirstToolWindow), 0, true);  
        if ((null == window) || (null == window.Frame))  
        {  
                            throw new NotSupportedException("Cannot create tool window");  
        }  
  
        IVsWindowFrame windowFrame = (IVsWindowFrame)window.Frame;  
                Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure(windowFrame.Show());  
  
         var mcs = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;  
        var toolbarbtnCmdID = new CommandID(new Guid(FirstToolWindowCommandguidFirstToolWindowPackageCmdSet),  
            FirstToolWindowCommand.cmdidWindowsMediaOpen);  
        var menuItem = new MenuCommand(new EventHandler(  
            ButtonHandler), toolbarbtnCmdID);  
        mcs.AddCommand(menuItem);  
    }  
    ```  
  
4. 添加按钮处理程序方法。 创建用户指定要播放的媒体文件的 OpenFileDialog 并播放所选的文件。  
  
    ```csharp  
    private void ButtonHandler(object sender, EventArgs arguments)  
    {  
        OpenFileDialog openFileDialog = new OpenFileDialog();  
        DialogResult result = openFileDialog.ShowDialog();  
        if (result == DialogResult.OK)  
        {  
            window.control.MediaPlayer.Source = new System.Uri(openFileDialog.FileName);  
        }  
    }  
    ```  
  
## <a name="set-the-default-position-for-the-tool-window"></a>设置工具窗口的默认位置  
 接下来，工具窗口在 IDE 中指定的默认位置。 工具窗口的配置信息已 FirstToolWindowPackage.cs 文件中。  
  
1. 在 FirstToolWindowPackage.cs，找到<xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute>特性，可以在`FirstToolWindowPackage`类，该类将 FirstToolWindow 类型传递给构造函数。 若要指定默认位置，必须将更多参数添加到下面的示例的构造函数中。  
  
    ```csharp  
    [ProvideToolWindow(typeof(FirstToolWindow),  
        Style = Microsoft.VisualStudio.Shell.VsDockStyle.Tabbed,  
        Window = "3ae79031-e1bc-11d0-8f78-00a0c9110057")]  
    ```  
  
     第一个命名的参数是`Style`，其值为`Tabbed`，这意味着窗口将在现有窗口中的选项卡。 停靠的位置由指定`Window`参数，这种情况下，n 的 GUID**解决方案资源管理器**。  
  
    > [!NOTE]
    > 有关在 IDE 中窗口的类型的详细信息，请参阅<xref:EnvDTE.vsWindowType>。  
  
## <a name="testing-the-tool-window"></a>测试工具窗口  
  
1. 按 f5 键以打开新的 Visual Studio 实验实例生成。  
  
2. 上**视图**菜单，依次指向**其他 Windows** ，然后单击**第一个工具窗口**。  
  
     媒体播放器工具窗口应在同一位置中打开**解决方案资源管理器**。 如果仍显示在前面所述的相同位置中，重置窗口布局 (**窗口 / 重置窗口布局**)。  
  
3. 在工具窗口中单击 （它具有搜索图标） 按钮。 选择一个支持声音或视频文件，例如，C:\windows\media\chimes.wav，然后按**打开**。  
  
     应该能听到钟声声音。  
  
## <a name="see-also"></a>请参阅  
 [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)
