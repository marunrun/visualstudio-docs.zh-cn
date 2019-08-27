---
title: 演练：创建 SDK 使用C#或 Visual Basic |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: ef96a249-5eef-402a-a8d5-d74cb49239bd
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CSharp
- VB
ms.openlocfilehash: 6bb9ae53dfb2e849c35c05fe5187cddcf301622c
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66312639"
---
# <a name="walkthrough-create-an-sdk-using-c-or-visual-basic"></a>演练：创建 SDK 使用C#或 Visual Basic
在本演练中，将了解如何使用 Visual C# 创建一个简单的数学库 SDK，然后打包 SDK 作为 Visual Studio 扩展 (VSIX)。 将完成以下过程：

- [若要创建 SimpleMath Windows 运行时组件](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md#createClassLibrary)

- [若要创建 SimpleMathVSIX 扩展项目](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md#createVSIX)
- [创建示例应用程序使用类库](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md#createSample)

## <a name="prerequisites"></a>系统必备
 要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅[Visual Studio SDK](../extensibility/visual-studio-sdk.md)。

## <a name="createClassLibrary"></a> 若要创建 SimpleMath Windows 运行时组件

1. 在菜单栏上，依次选择“文件”   > “新建”   > “项目”  。

2. 在模板列表中，展开**Visual C#** 或**Visual Basic**，选择**Windows 应用商店**节点，然后选择**Windows 运行时组件**模板。

3. 在中**名称**框中，指定**SimpleMath**，然后选择**确定**按钮。

4. 在中**解决方案资源管理器**，打开快捷菜单**SimpleMath**项目节点，然后选择**属性**。

5. 重命名**Class1.cs**到**Arithmetic.cs**并更新它，以匹配下面的代码：

    [!code-csharp[CreatingAnSDKUsingWinRT#3](../extensibility/codesnippet/CSharp/walkthrough-creating-an-sdk-using-csharp-or-visual-basic_1.cs)]
    [!code-vb[CreatingAnSDKUsingWinRT#3](../extensibility/codesnippet/VisualBasic/walkthrough-creating-an-sdk-using-csharp-or-visual-basic_1.vb)]

6. 在中**解决方案资源管理器**，打开快捷菜单**解决方案 SimpleMath**节点，然后选择**Configuration Manager**。

    **Configuration Manager**对话框随即打开。

7. 在中**活动解决方案配置**列表中，选择**发行**。

8. 在**配置**列中，确认**SimpleMath**行设置为**版本**，然后选择**关闭**按钮以接受更改。

   > [!IMPORTANT]
   > SDK for SimpleMath 组件包括只有一个配置。 此配置中必须是发布版本，或使用该组件的应用程序不会通过认证[!INCLUDE[win8_appstore_long](../debugger/includes/win8_appstore_long_md.md)]。

9. 在中**解决方案资源管理器**，打开快捷菜单**SimpleMath**项目节点，然后选择**生成**。

## <a name="createVSIX"></a> 若要创建 SimpleMathVSIX 扩展项目

1. 上的快捷菜单**解决方案 SimpleMath**节点，选择**添加** > **新建项目**。

2. 在模板列表中，展开**Visual C#** 或**Visual Basic**，选择**扩展性**节点，然后选择**VSIX 项目**模板。

3. 在中**名称**框中，指定**SimpleMathVSIX**，然后选择**确定**按钮。

4. 在中**解决方案资源管理器**，选择**source.extension.vsixmanifest**项。

5. 在菜单栏上，选择“视图”   > “代码”  。

6. 现有的 XML 替换为以下 XML:

     [!code-xml[CreatingAnSDKUsingWinRT#1](../extensibility/codesnippet/XML/walkthrough-creating-an-sdk-using-csharp-or-visual-basic_2.xml)]

7. 在中**解决方案资源管理器**，选择**SimpleMathVSIX**项目。

8. 在菜单栏上，依次选择“项目”   > “添加新项”  。

9. 在列表中**常见项**，展开**数据**，然后选择**XML 文件**。

10. 在中**名称**框中，指定`SDKManifest.xml`，然后选择**添加**按钮。

11. 在中**解决方案资源管理器**，打开快捷菜单`SDKManifest.xml`，选择**属性**，然后将更改的值**包含在 VSIX**属性设置为 **，则返回 true**。

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

    **Visual Basic**

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

13. 在中**解决方案资源管理器**，打开快捷菜单**SimpleMathVSIX**项目中，选择**添加**，然后选择**新文件夹**。

14. 重命名该文件夹以`references`。

15. 打开快捷菜单**引用**文件夹中，选择**添加**，然后选择**新文件夹**。

16. 重命名文件夹的子`commonconfiguration`，创建的子文件夹中，并将命名的子文件夹`neutral`。

17. 重复前面的四个步骤，这一次重命名的第一个文件夹到`redist`。

     项目现在包含以下文件夹结构：

    ```xml
    references\commonconfiguration\neutral
    redist\commonconfiguration\neutral
    ```

18. 在中**解决方案资源管理器**，打开快捷菜单**SimpleMath**项目，，然后选择**在文件资源管理器中打开文件夹**。

19. 在中**文件资源管理器**，导航到*bin\Release*文件夹中，打开快捷菜单**SimpleMath.winmd**文件中，，然后选择**复制**.

20. 在中**解决方案资源管理器**，将文件粘贴到*references\commonconfiguration\neutral*文件夹中的**SimpleMathVSIX**项目。

21. 重复上一步骤中，粘贴**SimpleMath.pri**到文件*redist\commonconfiguration\neutral*文件夹中的**SimpleMathVSIX**项目。

22. 在中**解决方案资源管理器**，选择**SimpleMath.winmd**。

23. 在菜单栏上依次选择**视图** > **属性**(键盘：选择**F4**密钥)。

24. 在**属性**窗口中，更改**生成操作**属性设置为**内容**，然后将更改**包含在 VSIX** 属性**True**。

25. 在中**解决方案资源管理器**，重复此过程**SimpleMath.pri**。

26. 在中**解决方案资源管理器**，选择**SimpleMathVSIX**项目。

27. 在菜单栏上依次选择**构建** > **生成 SimpleMathVSIX**。

28. 在中**解决方案资源管理器**，打开快捷菜单**SimpleMathVSIX**项目，，然后选择**在文件资源管理器中打开文件夹**。

29. 在中**文件资源管理器**，导航到 *\bin\Release*文件夹，然后运行*SimpleMathVSIX.vsix*进行安装。

30. 选择**安装**按钮，等待安装完成，然后再重新启动 Visual Studio。

## <a name="createSample"></a> 创建示例应用程序使用类库

1. 在菜单栏上，依次选择“文件”   > “新建”   > “项目”  。

2. 在模板列表中，展开**Visual C#** 或**Visual Basic**，然后选择**Windows 应用商店**节点。

3. 选择**空白应用**模板，将项目命名**ArithmeticUI**，然后选择**确定**按钮。

4. 在中**解决方案资源管理器**，打开快捷菜单**ArithmeticUI**项目，，然后选择**添加** > **引用**.

5. 在引用类型的列表中，展开**Windows**，然后选择**扩展**。

6. 在细节窗格中，选择**WinRT 数学库**扩展。

    有关 SDK 的其他信息将出现。 你可以选择**详细信息**链接以打开 https://msdn.microsoft.com/，如在本演练前面在 SDKManifest.xml 文件中指定。

7. 在中**引用管理器**对话框中，选择**WinRT 数学库**复选框，，然后选择**确定**按钮。

8. 在菜单栏上依次选择**视图** > **对象浏览器**。

9. 在中**浏览**列表中，选择**简单的数学运算**。

     你现在可以浏览什么是 SDK 中。

10. 在中**解决方案资源管理器**，打开**MainPage.xaml**，并将其内容替换为以下 XAML:

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

    **Visual Basic**

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

11. 更新**MainPage.xaml.cs**以匹配下面的代码：

     [!code-csharp[CreatingAnSDKUsingWinRTDemoApp#2](../extensibility/codesnippet/CSharp/walkthrough-creating-an-sdk-using-csharp-or-visual-basic_5.cs)]
     [!code-vb[CreatingAnSDKUsingWinRTDemoApp#2](../extensibility/codesnippet/VisualBasic/walkthrough-creating-an-sdk-using-csharp-or-visual-basic_5.vb)]

12. 选择**F5**键运行应用程序。

13. 在应用中，输入任何两个数字，选择一个操作，然后选择 **=** 按钮。

     将显示正确的结果。

    已成功创建并使用扩展 SDK。

## <a name="see-also"></a>请参阅
- [演练：使用 SDK 创建C++](../extensibility/walkthrough-creating-an-sdk-using-cpp.md)
- [演练：创建使用 JavaScript SDK](../extensibility/walkthrough-creating-an-sdk-using-javascript.md)
- [创建软件开发工具包](../extensibility/creating-a-software-development-kit.md)
