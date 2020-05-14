---
title: 添加工具窗口 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- tutorials
- tool windows
ms.assetid: 8e16c381-03c8-404e-92ef-3614cdf3150a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 573f01043d8b1b0c2293a3ebf6e0c246a8727d6a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740263"
---
# <a name="add-a-tool-window"></a>添加工具窗口

在本演练中，您将了解如何创建工具窗口，并通过以下方式将其集成到 Visual Studio 中：

- 向工具窗口添加控件。

- 向工具窗口添加工具栏。

- 向工具栏添加命令。

- 实现命令。

- 设置工具窗口的默认位置。

## <a name="prerequisites"></a>先决条件

可视化工作室 SDK 作为可选功能包含在可视化工作室设置中。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-tool-window"></a>创建工具窗口

1. 使用 VSIX 模板创建名为**FirstToolWin**的项目，并添加名为**FirstToolWindow**的自定义工具窗口项模板。

    > [!NOTE]
    > 有关使用工具窗口创建扩展的详细信息，请参阅[使用工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)。

## <a name="add-a-control-to-the-tool-window"></a>向工具窗口添加控件

1. 删除默认控件。 打开*第一工具窗口控制.xaml*并删除 **"单击我" ！** 按钮。

2. 在 **"工具箱**"中，**展开"所有 WPF 控件"** 部分，并将**媒体元素**控件拖动到 **"第一工具窗口控制"** 窗体。 选择控件，并在 **"属性"** 窗口中命名此元素**mediaElement1**。

## <a name="add-a-toolbar-to-the-tool-window"></a>向工具窗口添加工具栏
通过按以下方式添加工具栏，可以保证其渐变和颜色与 IDE 的其余部分一致。

1. 在**解决方案资源管理器中**，打开*第一工具窗口包.vsct*。 *.vsct*文件使用 XML 定义工具窗口中的图形用户界面 （GUI） 元素。

2. 在"`<Symbols>`部分"中，`<GuidSymbol>`查找其`name`属性为`guidFirstToolWindowPackageCmdSet`的节点。 将以下两`<IDSymbol>`个元素添加到此节点中`<IDSymbol>`的元素列表中，以定义工具栏和工具栏组。

    ```xml
    <IDSymbol name="ToolbarID" value="0x1000" />
    <IDSymbol name="ToolbarGroupID" value="0x1001" />
    ```

3. 在`<Buttons>`节的正上方，创建`<Menus>`类似于的节：

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

    有几个不同类型的菜单。 此菜单是工具窗口中的工具栏，由其`type`属性定义。 和`guid``id`设置构成工具栏完全限定的 ID。 通常，`<Parent>`菜单的包含组。 但是，工具栏定义为其自己的父工具栏。 因此，相同的标识符用于`<Menu>`和`<Parent>`元素。 属性`priority`只是"0"。

4. 工具栏在许多方面类似于菜单。 例如，正如菜单可能具有命令组一样，工具栏也可能具有组。 （在菜单上，命令组由水平线分隔。 在工具栏上，组不由可视分隔符分隔。

    添加包含`<Groups>`元素的`<Group>`节。 这将定义您在节中声明其 ID 的`<Symbols>`组。 在`<Groups>``<Menus>`节后添加节。

    ```xml
    <Groups>
        <Group guid="guidFirstToolWindowPackageCmdSet" id="ToolbarGroupID" priority="0x0000">
            <Parent guid="guidFirstToolWindowPackageCmdSet" id="ToolbarID" />
        </Group>
    </Groups>
    ```

    通过将父 GUID 和 ID 设置为工具栏的 GUID 和 ID，将组添加到工具栏。

## <a name="add-a-command-to-the-toolbar"></a>向工具栏添加命令

向工具栏添加命令，该工具栏显示为按钮。

1. 在本`<Symbols>`节中，在工具栏和工具栏组声明之后声明以下 IDSymbol 元素。

    ```xml
    <IDSymbol name="cmdidWindowsMedia" value="0x0100" />
    <IDSymbol name="cmdidWindowsMediaOpen" value="0x132" />
    ```

2. 在`<Buttons>`节内添加按钮元素。 此元素将显示在工具窗口中的工具栏上，并带有 **"搜索**（放大镜）"图标。

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

3. 打开*FirstToolWindowCommand.cs，* 并在现有字段之后在类中添加以下行。

    ```csharp
    public const string guidFirstToolWindowPackageCmdSet = "00000000-0000-0000-0000-0000";  // get the GUID from the .vsct file
    public const uint cmdidWindowsMedia = 0x100;
    public const int cmdidWindowsMediaOpen = 0x132;
    public const int ToolbarID = 0x1000;
    ```

    这样做会使命令在代码中可用。

## <a name="add-a-mediaplayer-property-to-firsttoolwindowcontrol"></a>将 MediaPlayer 属性添加到第一工具窗口控制
从工具栏控件的事件处理程序中，代码必须能够访问媒体播放器控件，该控件是 FirstToolWindowControl 类的子级。

在**解决方案资源管理器**中，右键单击*FirstToolWindowControl.xaml，* 单击 **"查看代码**"，并将以下代码添加到 FirstToolWindowControl 类。

```csharp
public System.Windows.Controls.MediaElement MediaPlayer
{
    get { return mediaElement1; }
}
```

## <a name="instantiate-the-tool-window-and-toolbar"></a>实例化工具窗口和工具栏
添加工具栏和菜单命令，用于调用 **"打开文件"** 对话框并播放选定的媒体文件。

1. 打开*FirstToolWindow.cs*并添加以下`using`指令：

    ```csharp
    using System.ComponentModel.Design;
    using System.Windows.Forms;
    using Microsoft.VisualStudio.Shell.Interop;
    ```

2. 在 FirstToolWindow 类中，添加对 FirstToolWindow 控制的公共引用。

    ```csharp
    public FirstToolWindowControl control;
    ```

3. 在构造函数的末尾，将此控件变量设置为新创建的控件。

    ```csharp
    control = new FirstToolWindowControl();
    base.Content = control;
    ```

4. 实例化构造函数内的工具栏。

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

6. 将菜单命令添加到工具栏。 在FirstToolWindowCommand.cs类中，添加以下使用指令：

    ```csharp
    using System.Windows.Forms;
    ```

7. 在 FirstToolWindowCommand 类中，在 ShowToolWindow（） 方法的末尾添加以下代码。 按钮处理程序命令将在下一节中实现。

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

1. 在第一ToolWindowCommand类中，添加一个按钮Handler方法，该方法调用**打开的文件**对话框。 选择文件后，它将播放媒体文件。

2. 在 FirstToolWindowCommand 类中，添加对在 FindToolWindow（） 方法中创建的 FirstToolWindow 窗口的私有引用。

    ```csharp
    private FirstToolWindow window;
    ```

3. 更改 ShowToolWindow（） 方法以设置上面定义的窗口（以便 ButtonHandler 命令处理程序可以访问窗口控件。 下面是完整的 ShowToolWindow（） 方法。

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

4. 添加 ButtonHandler 方法。 它创建一个 OpenFileDialog 供用户指定要播放的媒体文件，然后播放所选文件。

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

接下来，在工具窗口的 IDE 中指定默认位置。 工具窗口的配置信息位于*FirstToolWindowPackage.cs*文件中。

1. 在*FirstToolWindowPackage.cs*，在<xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute>类上`FirstToolWindowPackage`查找属性，该属性将 FirstToolWindow 类型传递给构造函数。 要指定默认位置，必须向下面的构造函数添加更多参数。

    ```csharp
    [ProvideToolWindow(typeof(FirstToolWindow),
        Style = Microsoft.VisualStudio.Shell.VsDockStyle.Tabbed,
        Window = "3ae79031-e1bc-11d0-8f78-00a0c9110057")]
    ```

    第一个命名参数`Style`是，其值`Tabbed`为 ，这意味着窗口将是现有窗口中的选项卡。 停靠位置由`Window`参数（n 本例）**指定，即解决方案资源管理器**的 GUID。

    > [!NOTE]
    > 有关 IDE 中窗口类型的详细信息，请参阅<xref:EnvDTE.vsWindowType>。

## <a name="test-the-tool-window"></a>测试工具窗口

1. 按**F5**打开可视化工作室实验构建的新实例。

2. 在 **"查看"** 菜单上，指向**其他窗口**，然后单击 **"第一个工具窗口**"。

    媒体播放器工具窗口应打开与**解决方案资源管理器**相同的位置。 如果它仍然显示与以前相同的位置，请重置窗口布局（**窗口/重置窗口布局**）。

3. 单击工具窗口中的按钮（具有 **"搜索**"图标）。 选择受支持的声音或视频文件，例如 *，C：\windows\media_chimes.wav，* 然后按 **"打开**"。

    你应该听到提示音。

## <a name="see-also"></a>请参阅
- [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)
