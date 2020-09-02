---
title: 将用户控件添加到起始页 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- start page dll
- custom start page
- start page assembly
ms.assetid: 5b7997db-af6f-4fa9-a128-bceb42bddaf1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 8000c6cc067f61a64c71b8c8ac4f5c0176504cd4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85903381"
---
# <a name="add-user-control-to-the-start-page"></a>将用户控件添加到起始页

此演练演示如何将 DLL 引用添加到自定义起始页。 该示例将用户控件添加到解决方案，生成用户控件，然后从起始页 *.xaml* 文件中引用生成的程序集。 新选项卡承载用户控件，该控件充当基本 Web 浏览器。

您可以使用相同的过程添加可从 *.xaml* 文件调用的任何程序集。

## <a name="add-a-wpf-user-control-to-the-solution"></a>向解决方案中添加 WPF 用户控件

首先，将 Windows Presentation Foundation (WPF) 用户控件添加到起始页解决方案。

1. 使用 " [创建自定义起始页](../extensibility/creating-a-custom-start-page.md)" 中创建的创建起始页。

2. 在 **解决方案资源管理器**中，右键单击解决方案，单击 " **添加**"，然后单击 " **新建项目**"。

3. 在 " **新建项目** " 对话框的左窗格中，展开 " **Visual Basic** " 或 " **Visual c #** " 节点，然后单击 " **Windows**"。 在中间窗格中，选择 " **WPF 用户控件库**"。

4. 为该控件命名 `WebUserControl` ，然后单击 **"确定"**。

## <a name="implement-the-user-control"></a>实现用户控件

若要实现 WPF 用户控件，请在 XAML 中 (UI) 生成用户界面，然后使用 c # 或其他 .NET 语言编写代码隐藏事件。

### <a name="to-write-the-xaml-for-the-user-control"></a>为用户控件编写 XAML

1. 打开用户控件的 XAML 文件。 在 `<Grid>` 元素中，将以下行定义添加到控件。

    ```vb
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="*" />
    </Grid.RowDefinitions>

    ```

2. 在主 `<Grid>` 元素中，添加以下新 `<Grid>` 元素，其中包含用于键入 Web 地址的文本框，以及用于设置新地址的按钮。

    ```xml
    <Grid Grid.Row="0">
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="*" />
            <ColumnDefinition Width="Auto" />
        </Grid.ColumnDefinitions>
        <TextBox x:Name="UserSource" Grid.Column="0" />
        <Button Grid.Column="1" x:Name="SetButton" Content="Set Address" Click="SetButton_Click" />
    </Grid>
    ```

3. 将以下框架添加到顶级 `<Grid>` 元素，只需在 `<Grid>` 包含按钮和文本框的元素之后。

    ```vb
    <Frame Grid.Row="1" x:Name="WebFrame" Source="http://www.bing.com" Navigated="WebFrame_Navigated" />
    ```

4. 下面的示例演示了用户控件的已完成 XAML。

    ```xml
    <UserControl x:Class="WebUserControl.UserControl1"
                 xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
                 xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
                 xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
                 xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
                 mc:Ignorable="d"
                 d:DesignHeight="300" d:DesignWidth="300">
        <Grid>
            <Grid.RowDefinitions>
                <RowDefinition Height="Auto"/>
                <RowDefinition Height="*" />
            </Grid.RowDefinitions>
            <Grid Grid.Row="0">
                <Grid.ColumnDefinitions>
                    <ColumnDefinition Width="*" />
                    <ColumnDefinition Width="Auto" />
                </Grid.ColumnDefinitions>
                <TextBox x:Name="UserSource" Grid.Column="0" />
                <Button Grid.Column="1" x:Name="SetButton" Content="Set Address" Click="SetButton_Click" />
            </Grid>
            <Frame Grid.Row="1" x:Name="WebFrame" Source="http://www.bing.com" Navigated="WebFrame_Navigated" />
        </Grid>
    </UserControl>

    ```

### <a name="to-write-the-code-behind-events-for-the-user-control"></a>为用户控件写入代码隐藏事件

1. 在 XAML 设计器中，双击添加到控件的 " **设置地址** " 按钮。

    *UserControl1.cs*文件将在代码编辑器中打开。

2. 按如下所示填写 SetButton_Click 事件处理程序。

    ```csharp
    private void SetButton_Click(object sender, RoutedEventArgs e)
    {
        try
        {
            this.WebFrame.Source = new Uri(this.UserSource.Text, UriKind.Absolute);
        }
        catch (Exception error)
        {
            MessageBox.Show(error.Message);
        }
    }
    ```

    此代码将文本框中键入的 Web 地址设置为 Web 浏览器的目标。 如果该地址无效，则代码将引发错误。

3. 还必须处理 WebFrame_Navigated 事件：

    ```csharp
    private void WebFrame_Navigated(object sender, EventArgs e)
    { }
    ```

4. 生成解决方案。

## <a name="add-the-user-control-to-the-start-page"></a>将用户控件添加到起始页

若要使此控件可用于 "起始页" 项目，请在 "起始页" 项目文件中添加对新控件库的引用。 然后，可以将该控件添加到起始页 XAML 标记。

1. 在 **解决方案资源管理器**的 "起始页" 项目中，右键单击 " **引用** "，然后单击 " **添加引用**"。

2. 在 " **项目** " 选项卡上，选择 " **WebUserControl** "，然后单击 **"确定"**。

3. 在“生成”菜单中，单击“生成解决方案”。

    生成解决方案使用户控件对解决方案中其他文件的 IntelliSense 可用。

    若要将控件添加到起始页 XAML 标记中，请添加对程序集的命名空间引用，然后将控件放置在该页上。

### <a name="to-add-the-control-to-the-markup"></a>向标记添加控件

1. 在 **解决方案资源管理器**中，打开起始页 *.xaml* 文件。

2. 在 " **XAML** " 窗格中，将以下命名空间声明添加到顶级 <xref:System.Windows.Controls.Grid> 元素。

   ```xml
   xmlns:vsc="clr-namespace:WebUserControl;assembly=WebUserControl"
   ```

3. 在 " **XAML** " 窗格中，滚动到 \<Grid> 部分。

    部分包含 <xref:System.Windows.Controls.TabControl> 元素中的元素 <xref:System.Windows.Controls.Grid> 。

4. 添加一个 \<TabControl> 元素 \<TabItem> ，该元素包含包含对用户控件的引用的。

    ```xml

    <TabItem Header="Web" Height="Auto">
        <vsc:UserControl1 />
    </TabItem>

    ```

    现在可以测试控件。

## <a name="test-a-manually-created-custom-start-page"></a>测试手动创建的自定义起始页

1. 将 XAML 文件和任何支持的文本文件或标记文件复制到 *%USERPROFILE%\My Documents\Visual Studio 2015 \ StartPages \\ *文件夹中。

2. 如果起始页引用 Visual Studio 未安装的程序集中的任何控件或类型，请复制这些程序集，然后将其粘贴到_Visual studio 安装文件夹_**\Common7\IDE\PrivateAssemblies \\ **中。

3. 在 Visual Studio 命令提示符处，键入 **devenv/Rootsuffix Exp** 来打开 Visual studio 的实验实例。

4. 在实验实例中，请切换到 "**工具**  >  **选项**  >  **环境**  >  **启动**" 页，然后从 "**自定义起始页**" 下拉列表中选择您的 XAML 文件。

5. 在“视图” **** 菜单上，单击“起始页” ****。

    应显示自定义起始页。 如果要更改任何文件，则必须关闭实验实例，进行更改，复制并粘贴已更改的文件，然后重新打开实验实例以查看更改。

## <a name="see-also"></a>另请参阅

- [WPF 容器控件](https://msdn.microsoft.com/library/a0177167-d7db-4205-9607-8ae316952566)
- [演练：将自定义 XAML 添加到起始页](../extensibility/walkthrough-adding-custom-xaml-to-the-start-page.md)
