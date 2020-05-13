---
title: 将用户控件添加到"开始"页 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: b426cfbbfca2e301797644a1fc73f188054d0cfa
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740126"
---
# <a name="add-user-control-to-the-start-page"></a>将用户控件添加到"开始页面"

本演练演示如何向自定义起始页添加 DLL 引用。 该示例将用户控件添加到解决方案，生成用户控件，然后从"起始页 *.xaml*文件"引用生成的程序集。 新选项卡承载用户控件，该控件充当基本 Web 浏览器。

可以使用同一进程添加可以从 *.xaml*文件调用的任何程序集。

## <a name="add-a-wpf-user-control-to-the-solution"></a>向解决方案添加 WPF 用户控件

首先，将 Windows 演示文稿基础 （WPF） 用户控件添加到"开始页"解决方案。

1. 使用我们在[创建自定义起始页](../extensibility/creating-a-custom-start-page.md)中创建的创建起始页。

2. 在 **"解决方案资源管理器"** 中，右键单击解决方案，单击"**添加**"，然后单击 **"新项目**"。

3. 在 **"新项目**"对话框的左侧窗格中，展开 **"可视基本"** 或 **"可视 C#"** 节点，然后单击**Windows**。 在中间窗格中，选择**WPF 用户控制库**。

4. 命名控件`WebUserControl`，然后单击 **"确定**"。

## <a name="implement-the-user-control"></a>实现用户控制

要实现 WPF 用户控件，请在 XAML 中构建用户界面 （UI），然后用 C# 或其他 .NET 语言编写代码背后的事件。

### <a name="to-write-the-xaml-for-the-user-control"></a>为用户控件编写 XAML

1. 打开用于用户控制的 XAML 文件。 在`<Grid>`元素中，向控件添加以下行定义。

    ```vb
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="*" />
    </Grid.RowDefinitions>

    ```

2. 在主`<Grid>`元素中，添加以下新`<Grid>`元素，其中包含用于键入 Web 地址的文本框和用于设置新地址的按钮。

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

3. 将以下框架添加到包含按钮和文本框`<Grid>``<Grid>`的元素之后的顶层元素。

    ```vb
    <Frame Grid.Row="1" x:Name="WebFrame" Source="http://www.bing.com" Navigated="WebFrame_Navigated" />
    ```

4. 下面的示例显示了用户控件的已完成的 XAML。

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

### <a name="to-write-the-code-behind-events-for-the-user-control"></a>为用户控件编写代码背后的事件

1. 在 XAML 设计器中，双击添加到控件的 **"设置地址"** 按钮。

    *UserControl1.cs*文件将在代码编辑器中打开。

2. 填写SetButton_Click事件处理程序，如下所示。

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

    此代码将文本框中键入的 Web 地址集为 Web 浏览器的目标。 如果地址无效，代码将引发错误。

3. 您还必须处理WebFrame_Navigated事件：

    ```csharp
    private void WebFrame_Navigated(object sender, EventArgs e)
    { }
    ```

4. 生成解决方案。

## <a name="add-the-user-control-to-the-start-page"></a>将用户控件添加到"开始页面"

要使此控件可用于"开始页"项目，在"开始页"项目文件中，添加对新控件库的引用。 然后，您可以将控件添加到起始页 XAML 标记。

1. 在 **"解决方案资源管理器**"中，在"开始页"项目中，右键单击 **"引用**"，然后单击"**添加参考**"。

2. 在"**项目"** 选项卡上，选择**WebUser 控制**，然后单击"**确定**"。

3. 在“生成”**** 菜单中，单击“生成解决方案”****。

    构建解决方案使 IntelliSense 可用于解决方案中的其他文件的用户控制。

    要将控件添加到"开始页 XAML 标记"，向程序集添加命名空间引用，然后将该控件放在页面上。

### <a name="to-add-the-control-to-the-markup"></a>将控件添加到标记

1. 在**解决方案资源管理器中**，打开起始页 *.xaml*文件。

2. 在**XAML**窗格中，将以下命名空间声明添加到顶级<xref:System.Windows.Controls.Grid>元素。

   ```xml
   xmlns:vsc="clr-namespace:WebUserControl;assembly=WebUserControl"
   ```

3. 在**XAML**窗格中，滚动\<到网格>部分。

    该节包含<xref:System.Windows.Controls.Grid>元素中<xref:System.Windows.Controls.TabControl>的元素。

4. 添加\<TabControl>元素，\<其中包含包含对用户控件的引用的 TabItem>。

    ```xml

    <TabItem Header="Web" Height="Auto">
        <vsc:UserControl1 />
    </TabItem>

    ```

    现在，您可以测试该控件。

## <a name="test-a-manually-created-custom-start-page"></a>测试手动创建的自定义开始页

1. 将 XAML 文件以及任何支持的文本文件或标记文件复制到 *%USERPROFILE%*我的文档_Visual Studio 2015_StartPages\\*文件夹。

2. 如果起始页引用 Visual Studio 未安装的程序集中的任何控件或类型，请复制程序集，然后将它们粘贴到_Visual Studio 安装文件夹_**[公共7_IDE\\私有程序集**中。

3. 在 Visual Studio 命令提示符中，键入**devenv /rootsuffix Exp**以打开 Visual Studio 的实验实例。

4. 在实验实例中，转到 **"工具** > **选项** > **环境** > **启动"** 页，然后从 **"自定义起始页"** 下拉列表中选择 XAML 文件。

5. 在“视图” **** 菜单上，单击“起始页” ****。

    应显示自定义起始页。 如果要更改任何文件，则必须关闭实验实例、进行更改、复制和粘贴已更改的文件，然后重新打开实验实例以查看更改。

## <a name="see-also"></a>请参阅

- [WPF 容器控件](https://msdn.microsoft.com/library/a0177167-d7db-4205-9607-8ae316952566)
- [演练：将自定义 XAML 添加到起始页](../extensibility/walkthrough-adding-custom-xaml-to-the-start-page.md)
