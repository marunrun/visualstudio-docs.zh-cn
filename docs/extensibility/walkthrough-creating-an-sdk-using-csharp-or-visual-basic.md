---
title: '演练：使用 c # 或 Visual Basic 创建 SDK |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: ef96a249-5eef-402a-a8d5-d74cb49239bd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CSharp
- VB
ms.openlocfilehash: 73cd76445adb798be078461e5b209e35f8b8163c
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904977"
---
# <a name="walkthrough-create-an-sdk-using-c-or-visual-basic"></a>演练：使用 c # 或 Visual Basic 创建 SDK
在本演练中，你将学习如何使用 Visual c # 创建一个简单的数学库 SDK，然后将 SDK 打包为 Visual Studio 扩展（VSIX）。 你将完成以下过程：

- [创建 SimpleMath Windows 运行时组件](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md#createClassLibrary)

- [创建 SimpleMathVSIX 扩展项目](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md#createVSIX)
- [创建使用类库的示例应用程序](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md#createSample)

## <a name="prerequisites"></a>必备条件
 要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅[Visual STUDIO SDK](../extensibility/visual-studio-sdk.md)。

## <a name="to-create-the-simplemath-windows-runtime-component"></a><a name="createClassLibrary"></a>创建 SimpleMath Windows 运行时组件

1. 在菜单栏上，依次选择“文件” > “新建” > “项目”。

2. 在模板列表中，展开 " **Visual c #** " 或 " **Visual Basic**"，选择 " **Windows 应用商店**" 节点，然后选择 " **Windows 运行时组件**" 模板。

3. 在 "**名称**" 框中，指定**SimpleMath**，然后选择 "**确定"** 按钮。

4. 在**解决方案资源管理器**中，打开**SimpleMath**项目节点的快捷菜单，然后选择 "**属性**"。

5. 将**Class1.cs**重命名为**Arithmetic.cs** ，并对其进行更新以匹配以下代码：

    [!code-csharp[CreatingAnSDKUsingWinRT#3](../extensibility/codesnippet/CSharp/walkthrough-creating-an-sdk-using-csharp-or-visual-basic_1.cs)]
    [!code-vb[CreatingAnSDKUsingWinRT#3](../extensibility/codesnippet/VisualBasic/walkthrough-creating-an-sdk-using-csharp-or-visual-basic_1.vb)]

6. 在**解决方案资源管理器**中，打开**解决方案 "SimpleMath"** 节点的快捷菜单，然后选择 " **Configuration Manager**"。

    此时将打开 " **Configuration Manager** " 对话框。

7. 在 "**活动解决方案配置**" 列表中，选择 "**发布**"。

8. 在 "**配置**" 列中，验证 " **SimpleMath** " 行是否设置为 "**发布**"，然后选择 "**关闭**" 按钮接受更改。

   > [!IMPORTANT]
   > SimpleMath 组件的 SDK 只包含一个配置。 此配置必须是发布版本，或使用组件的应用不会通过证书 [!INCLUDE[win8_appstore_long](../debugger/includes/win8_appstore_long_md.md)] 。

9. 在**解决方案资源管理器**中，打开**SimpleMath**项目节点的快捷菜单，然后选择 "**生成**"。

## <a name="to-create-the-simplemathvsix-extension-project"></a><a name="createVSIX"></a>创建 SimpleMathVSIX 扩展项目

1. 在**解决方案 "SimpleMath"** 节点的快捷菜单上，选择 "**添加**  >  **新项目**"。

2. 在模板列表中，展开 " **Visual c #** " 或 " **Visual Basic**"，选择 "**扩展性**" 节点，然后选择 " **VSIX 项目**" 模板。

3. 在 "**名称**" 框中，指定**SimpleMathVSIX**，然后选择 "**确定"** 按钮。

4. 在**解决方案资源管理器**中，选择**source.extension.vsixmanifest**项。

5. 在菜单栏上，选择 "**查看**  >  **代码**"。

6. 将现有的 XML 替换为以下 XML：

     [!code-xml[CreatingAnSDKUsingWinRT#1](../extensibility/codesnippet/XML/walkthrough-creating-an-sdk-using-csharp-or-visual-basic_2.xml)]

7. 在**解决方案资源管理器**中，选择 " **SimpleMathVSIX** " 项目。

8. 在菜单栏上，选择 "**项目**" "  >  **添加新项**"。

9. 在**常见项**列表中，展开 "**数据**"，然后选择 " **XML 文件**"。

10. 在 "**名称**" 框中，指定 `SDKManifest.xml` ，然后选择 "**添加**" 按钮。

11. 在**解决方案资源管理器**中，打开的快捷菜单 `SDKManifest.xml` ，选择 "**属性**"，然后将 "**包括在 VSIX 中**" 属性的值更改为 " **True**"。

12. 用下列 XML 替换该文件的内容：

    **C#**

    ```xml
    <FileList
      DisplayName="WinRT Math Library (CS)"
      MinVSVersion="11.0"
      TargetFramework=".NETCore,version=v4.5"
      AppliesTo="WindowsAppContainer"
      SupportsMultipleVersions="Error"
      MoreInfo="https://msdn.microsoft.com/">
    </FileList>
    ```

    Visual Basic

    ```xml
    <FileList
      DisplayName="WinRT Math Library (VB)"
      MinVSVersion="11.0"
      TargetFramework=".NETCore,version=v4.5"
      AppliesTo="WindowsAppContainer"
      SupportsMultipleVersions="Error"
      MoreInfo="https://msdn.microsoft.com/">
    </FileList>
    ```

13. 在**解决方案资源管理器**中，打开**SimpleMathVSIX**项目的快捷菜单，选择 "**添加**"，然后选择 "**新建文件夹**"。

14. 将文件夹重命名为 `references` 。

15. 打开 "**引用**" 文件夹的快捷菜单，选择 "**添加**"，然后选择 "**新建文件夹**"。

16. 将子文件夹重命名为 `commonconfiguration` ，在其中创建子文件夹，并将子文件夹命名为 `neutral` 。

17. 重复前面的四个步骤，这次将第一个文件夹重命名为 `redist` 。

     该项目现在包含以下文件夹结构：

    ```xml
    references\commonconfiguration\neutral
    redist\commonconfiguration\neutral
    ```

18. 在**解决方案资源管理器**中，打开**SimpleMath**项目的快捷菜单，然后选择 "**在文件资源管理器中打开文件夹**"。

19. 在**文件资源管理器**中，导航到*bin\Release*文件夹，打开**SimpleMath**文件的快捷菜单，然后选择 "**复制**"。

20. 在**解决方案资源管理器**中，将该文件粘贴到**SimpleMathVSIX**项目的*references\commonconfiguration\neutral*文件夹中。

21. 重复上一步，将**SimpleMath**文件粘贴到**SimpleMathVSIX**项目中的*redist\commonconfiguration\neutral*文件夹。

22. 在**解决方案资源管理器**中，选择 " **SimpleMath**"。

23. 在菜单栏上，选择 "**查看**  >  **属性**" （键盘：选择**F4**键）。

24. 在 "**属性**" 窗口中，将 "**生成操作**" 属性更改为 "**内容**"，然后将 "**包括在 VSIX 中**" 属性更改为**True**。

25. 在**解决方案资源管理器**中，对**SimpleMath**重复此过程。

26. 在**解决方案资源管理器**中，选择 " **SimpleMathVSIX** " 项目。

27. 在菜单栏上，选择 "**生成**  >  **生成 SimpleMathVSIX**"。

28. 在**解决方案资源管理器**中，打开**SimpleMathVSIX**项目的快捷菜单，然后选择 "**在文件资源管理器中打开文件夹**"。

29. 在**文件资源管理器**中，导航到*\bin\Release*文件夹，然后运行*SimpleMathVSIX*安装。

30. 选择 "**安装**" 按钮，等待安装完成，然后重启 Visual Studio。

## <a name="to-create-a-sample-app-that-uses-the-class-library"></a><a name="createSample"></a>创建使用类库的示例应用程序

1. 在菜单栏上，依次选择“文件” > “新建” > “项目”。

2. 在模板列表中，展开 " **Visual c #** " 或 " **Visual Basic**"，然后选择 " **Windows 应用商店**" 节点。

3. 选择 "**空白应用**" 模板，将项目命名为 " **ArithmeticUI**"，然后选择 **"确定"** 按钮。

4. 在**解决方案资源管理器**中，打开**ArithmeticUI**项目的快捷菜单，然后选择 "**添加**  >  **引用**"。

5. 在引用类型列表中，展开 " **Windows**"，然后选择 "**扩展**"。

6. 在详细信息窗格中，选择 " **WinRT 数学库**" 扩展。

    此时会显示有关 SDK 的更多信息。 你可以选择 "**详细信息**" 链接打开 https://msdn.microsoft.com/ ，如本演练前面的 SDKManifest.xml 文件中所指定的那样。

7. 在 "**引用管理器**" 对话框中，选中 " **WinRT 数学库**" 复选框，然后选择 **"确定"** 按钮。

8. 在菜单栏上，选择 "**查看**  >  **对象浏览器**"。

9. 在 "**浏览**" 列表中，选择 "**简单数学**"。

     你现在可以浏览 SDK 中的内容。

10. 在**解决方案资源管理器**中，打开**MainPage**，并将其内容替换为以下 xaml：

    **C#**

    ```xml
    <Page
        x:Class="ArithmeticUI.MainPage"
        IsTabStop="False"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:local="using:SimpleMath"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        mc:Ignorable="d">

        <Grid Background="{StaticResource ApplicationPageBackgroundThemeBrush}">
            <TextBox x:Name="_firstNumber" HorizontalAlignment="Left" Margin="414,370,0,0" TextWrapping="Wrap" Text="First Number" VerticalAlignment="Top" Height="32" Width="135" TextAlignment="Center"/>
            <TextBox x:Name="_secondNumber" HorizontalAlignment="Left" Margin="613,370,0,0" TextWrapping="Wrap" Text="Second Number" VerticalAlignment="Top" Height="32" Width="135" TextAlignment="Center"/>
            <Button Content="+" HorizontalAlignment="Left" Margin="557,301,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnOperatorClick"/>
            <Button Content="-" HorizontalAlignment="Left" Margin="557,345,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnOperatorClick"/>
            <Button Content="*" HorizontalAlignment="Left" Margin="557,389,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnOperatorClick"/>
            <Button Content="/" HorizontalAlignment="Left" Margin="557,433,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnOperatorClick"/>
            <Button Content="=" HorizontalAlignment="Left" Margin="755,367,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnResultsClick"/>
            <TextBox x:Name="_result" HorizontalAlignment="Left" Margin="809,370,0,0" TextWrapping="Wrap" Text="Result" VerticalAlignment="Top" Height="32" Width="163" TextAlignment="Center" IsReadOnly="True"/>
        </Grid>
    </Page>
    ```

    Visual Basic

    ```xml
    <Page
        x:Class="ArithmeticUI.MainPage"
        IsTabStop="False"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:local="using:SimpleMath"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        mc:Ignorable="d">

        <Grid Background="{StaticResource ApplicationPageBackgroundThemeBrush}">
            <TextBox x:Name="_firstNumber" HorizontalAlignment="Left" Margin="414,370,0,0" TextWrapping="Wrap" Text="First Number" VerticalAlignment="Top" Height="32" Width="135" TextAlignment="Center"/>
            <TextBox x:Name="_secondNumber" HorizontalAlignment="Left" Margin="613,370,0,0" TextWrapping="Wrap" Text="Second Number" VerticalAlignment="Top" Height="32" Width="135" TextAlignment="Center"/>
            <Button Content="+" HorizontalAlignment="Left" Margin="557,301,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnOperatorClick"/>
            <Button Content="-" HorizontalAlignment="Left" Margin="557,345,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnOperatorClick"/>
            <Button Content="*" HorizontalAlignment="Left" Margin="557,389,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnOperatorClick"/>
            <Button Content="/" HorizontalAlignment="Left" Margin="557,433,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnOperatorClick"/>
            <Button Content="=" HorizontalAlignment="Left" Margin="755,367,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnResultsClick"/>
            <TextBox x:Name="_result" HorizontalAlignment="Left" Margin="809,370,0,0" TextWrapping="Wrap" Text="Result" VerticalAlignment="Top" Height="32" Width="163" TextAlignment="Center" IsReadOnly="True"/>
        </Grid>
    </Page>
    ```

11. 更新**MainPage.xaml.cs**以匹配以下代码：

     [!code-csharp[CreatingAnSDKUsingWinRTDemoApp#2](../extensibility/codesnippet/CSharp/walkthrough-creating-an-sdk-using-csharp-or-visual-basic_5.cs)]
     [!code-vb[CreatingAnSDKUsingWinRTDemoApp#2](../extensibility/codesnippet/VisualBasic/walkthrough-creating-an-sdk-using-csharp-or-visual-basic_5.vb)]

12. 选择**F5**键以运行应用。

13. 在应用程序中，输入任意两个数字，选择一个操作，然后选择 **=** 按钮。

     显示正确的结果。

    你已成功创建并使用了扩展 SDK。

## <a name="see-also"></a>另请参阅
- [演练：使用 c + + 创建 SDK](../extensibility/walkthrough-creating-an-sdk-using-cpp.md)
- [演练：使用 JavaScript 创建 SDK](../extensibility/walkthrough-creating-an-sdk-using-javascript.md)
- [创建软件开发工具包](../extensibility/creating-a-software-development-kit.md)
