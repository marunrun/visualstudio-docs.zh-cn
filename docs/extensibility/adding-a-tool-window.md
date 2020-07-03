---
title: 添加工具窗口 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- tutorials
- tool windows
ms.assetid: 8e16c381-03c8-404e-92ef-3614cdf3150a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 169f386128ccdd79aef6b90a6703f50323b9b6f3
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904142"
---
# <a name="add-a-tool-window"></a>添加工具窗口

在本演练中，你将了解如何创建一个工具窗口，并通过以下方式将其集成到 Visual Studio 中：

- 将控件添加到工具窗口。

- 将工具栏添加到工具窗口。

- 向工具栏添加命令。

- 实现命令。

- 设置工具窗口的默认位置。

## <a name="prerequisites"></a>必备条件

Visual Studio SDK 作为 Visual Studio 安装程序中的可选功能提供。 有关详细信息，请参阅[安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-tool-window"></a>创建工具窗口

1. 使用 VSIX 模板创建名为**FirstToolWin**的项目，并添加一个名为**FirstToolWindow**的自定义工具窗口项模板。

    > [!NOTE]
    > 有关使用工具窗口创建扩展的详细信息，请参阅[使用工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)。

## <a name="add-a-control-to-the-tool-window"></a>向工具窗口添加控件

1. 删除默认控件。 打开*FirstToolWindowControl*并删除 "**单击我！** " 按钮。

2. 在 "**工具箱**" 中，展开 "**所有 WPF 控件**" 部分，然后将 "**媒体元素**" 控件拖动到 " **FirstToolWindowControl** " 窗体。 选择控件，然后在 "**属性**" 窗口中，将此元素命名为**mediaElement1**。

## <a name="add-a-toolbar-to-the-tool-window"></a>将工具栏添加到工具窗口
通过以下列方式添加工具栏，可保证其梯度和颜色与 IDE 的其余部分保持一致。

1. 在**解决方案资源管理器**中，打开 *.vsct*。 *.Vsct*文件使用 XML 定义工具窗口中的图形用户界面（GUI）元素。

2. 在 `<Symbols>` 部分中，找到 `<GuidSymbol>` `name` 属性为的节点 `guidFirstToolWindowPackageCmdSet` 。 将以下两个 `<IDSymbol>` 元素添加到 `<IDSymbol>` 此节点中的元素列表，以定义工具栏和工具栏组。

    ```xml
    <IDSymbol name="ToolbarID" value="0x1000" />
    <IDSymbol name="ToolbarGroupID" value="0x1001" />
    ```

3. 在该部分的正上方 `<Buttons>` ，创建一个 `<Menus>` 类似于下面的内容：

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

    有几种不同类型的菜单。 此菜单是工具窗口中的一个工具栏，由其 `type` 属性定义。 `guid`和 `id` 设置构成了工具栏的完全限定 ID。 通常， `<Parent>` 菜单的是包含组。 但是，工具栏定义为其自身的父级。 因此，同一标识符用于 `<Menu>` 和 `<Parent>` 元素。 此 `priority` 属性只是 "0"。

4. 工具栏类似于菜单。 例如，正如菜单可能包含命令组，工具栏也可能具有组。 （在菜单上，命令组由水平线分隔。 在工具栏上，组不是由视觉分隔符分隔的。）

    添加 `<Groups>` 包含元素的部分 `<Group>` 。 这会定义在部分中声明其 ID 的组 `<Symbols>` 。 将节添加到 `<Groups>` 节的紧后面 `<Menus>` 。

    ```xml
    <Groups>
        <Group guid="guidFirstToolWindowPackageCmdSet" id="ToolbarGroupID" priority="0x0000">
            <Parent guid="guidFirstToolWindowPackageCmdSet" id="ToolbarID" />
        </Group>
    </Groups>
    ```

    通过将父 GUID 和 ID 设置为工具栏的 GUID 和 ID，可以将组添加到工具栏中。

## <a name="add-a-command-to-the-toolbar"></a>将命令添加到工具栏

将命令添加到工具栏，该工具栏显示为按钮。

1. 在 `<Symbols>` 部分中，将以下 IDSymbol 元素声明在工具栏和工具栏组声明之后。

    ```xml
    <IDSymbol name="cmdidWindowsMedia" value="0x0100" />
    <IDSymbol name="cmdidWindowsMediaOpen" value="0x132" />
    ```

2. 在部分中添加 Button 元素 `<Buttons>` 。 此元素将显示在工具窗口中的工具栏上，并带有**搜索**（放大镜）图标。

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

3. 打开*FirstToolWindowCommand.cs* ，并在类中的现有字段之后添加以下行。

    ```csharp
    public const string guidFirstToolWindowPackageCmdSet = "00000000-0000-0000-0000-0000";  // get the GUID from the .vsct file
    public const uint cmdidWindowsMedia = 0x100;
    public const int cmdidWindowsMediaOpen = 0x132;
    public const int ToolbarID = 0x1000;
    ```

    这样做可以在代码中使用命令。

## <a name="add-a-mediaplayer-property-to-firsttoolwindowcontrol"></a>将 MediaPlayer 属性添加到 FirstToolWindowControl
在工具栏控件的事件处理程序中，你的代码必须能够访问 Media Player 控件，该控件是 FirstToolWindowControl 类的子控件。

在**解决方案资源管理器**中，右键单击*FirstToolWindowControl*，单击 "**查看代码**"，然后将以下代码添加到 FirstToolWindowControl 类。

```csharp
public System.Windows.Controls.MediaElement MediaPlayer
{
    get { return mediaElement1; }
}
```

## <a name="instantiate-the-tool-window-and-toolbar"></a>实例化工具窗口和工具栏
添加用于调用 "**打开文件**" 对话框并播放所选媒体文件的工具栏和菜单命令。

1. 打开*FirstToolWindow.cs* ，添加以下 `using` 指令：

    ```csharp
    using System.ComponentModel.Design;
    using System.Windows.Forms;
    using Microsoft.VisualStudio.Shell.Interop;
    ```

2. 在 FirstToolWindow 类中，添加对 FirstToolWindowControl 控件的公开引用。

    ```csharp
    public FirstToolWindowControl control;
    ```

3. 在构造函数的末尾，将此控件变量设置为新创建的控件。

    ```csharp
    control = new FirstToolWindowControl();
    base.Content = control;
    ```

4. 在构造函数中实例化工具栏。

    ```csharp
    this.ToolBar = new CommandID(new Guid(FirstToolWindowCommand.guidFirstToolWindowPackageCmdSet),
        FirstToolWindowCommand.ToolbarID);
    this.ToolBarLocation = (int)VSTWT_LOCATION.VSTWT_TOP;
    ```

5. 此时，FirstToolWindow 构造函数应如下所示：

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

6. 向工具栏添加菜单命令。 在 FirstToolWindowCommand.cs 类中，添加以下 using 指令：

    ```csharp
    using System.Windows.Forms;
    ```

7. 在 FirstToolWindowCommand 类中，在 ShowToolWindow （）方法的末尾添加以下代码。 下一节将实现 ButtonHandler 命令。

    ```csharp
    // Create the handles for the toolbar command.
    var mcs = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;
    var toolbarbtnCmdID = new CommandID(new Guid(FirstToolWindowCommand.guidFirstToolWindowPackageCmdSet),
        FirstToolWindowCommand.cmdidWindowsMediaOpen);
    var menuItem = new MenuCommand(new EventHandler(
        ButtonHandler), toolbarbtnCmdID);
    mcs.AddCommand(menuItem);
    ```

### <a name="to-implement-a-menu-command-in-the-tool-window"></a>在工具窗口中实现菜单命令

1. 在 FirstToolWindowCommand 类中，添加调用 "**打开文件**" 对话框的 ButtonHandler 方法。 选择文件后，它会播放媒体文件。

2. 在 FirstToolWindowCommand 类中，添加对在 FindToolWindow （）方法中创建的 FirstToolWindow 窗口的私有引用。

    ```csharp
    private FirstToolWindow window;
    ```

3. 更改 ShowToolWindow （）方法以设置前面定义的窗口（以便 ButtonHandler 命令处理程序可以访问窗口控件）。 下面是完整的 ShowToolWindow （）方法。

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

4. 添加 ButtonHandler 方法。 它将为用户创建 OpenFileDialog 以指定要播放的媒体文件，然后播放所选文件。

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

接下来，在 IDE 中指定工具窗口的默认位置。 工具窗口的配置信息位于*FirstToolWindowPackage.cs*文件中。

1. 在*FirstToolWindowPackage.cs*中，找到 <xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute> 类的属性，该属性将 `FirstToolWindowPackage` FirstToolWindow 类型传递给构造函数。 若要指定默认位置，必须在下面的示例中向构造函数添加更多参数。

    ```csharp
    [ProvideToolWindow(typeof(FirstToolWindow),
        Style = Microsoft.VisualStudio.Shell.VsDockStyle.Tabbed,
        Window = "3ae79031-e1bc-11d0-8f78-00a0c9110057")]
    ```

    第一个命名参数为 `Style` ，其值为 `Tabbed` ，这意味着窗口将是现有窗口中的一个选项卡。 停靠位置由 `Window` 参数指定，即 n 本例中**解决方案资源管理器**的 GUID。

    > [!NOTE]
    > 有关 IDE 中的窗口类型的详细信息，请参阅 <xref:EnvDTE.vsWindowType> 。

## <a name="test-the-tool-window"></a>测试工具窗口

1. 按**F5**打开 Visual Studio 实验生成的新实例。

2. 在 "**视图**" 菜单上，指向 "**其他窗口**"，再单击 "**第一个工具窗口**"。

    Media player 工具窗口应在与**解决方案资源管理器**相同的位置打开。 如果它仍显示在与以前相同的位置，则重置窗口布局（**窗口/重置窗口布局**）。

3. 单击工具窗口中的按钮（它具有**搜索**图标）。 选择受支持的声音或视频文件，例如 " *C:\windows\media\chimes.wav*"，然后按 "**打开**"。

    你应该会听到钟声声音。

## <a name="see-also"></a>另请参阅
- [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)
