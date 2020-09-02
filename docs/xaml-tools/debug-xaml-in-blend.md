---
title: 在 Blend 中调试 XAML |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 29a37182-2a2c-47e4-a4a9-2d5412738fed
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- uwp
ms.openlocfilehash: d5d40878e40641b9a54a411af122f6207a02a7a1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85331032"
---
# <a name="debug-xaml-in-blend"></a>在 Blend 中调试 XAML

可以使用 Blend for Visual Studio 中的工具在应用中调试 XAML。 生成项目时，任何错误都会在“结果”面板中显示****。 双击一个错误可找到与该错误相关的标记。 如果需要更多的工作空间，可以通过按**F12**隐藏**结果**面板。

## <a name="syntax-errors"></a>语法错误

如果 XAML 或代码隐藏文件不符合语言的格式设置规则，则将出现语法错误。 错误的说明有助于理解如何更正该错误。 该列表还指定了出现错误的文件名称和行号。 XAML 错误会在“结果”面板的“标记”选项卡上列出********。

> [!TIP]
> XAML 是一个基于 XML 的标记语言并遵循 XML 语法规则。

XAML 语法错误的某些常见原因如下：

- 关键字的拼写错误或大小写错误。

- 特性或文本字符串前后丢失问号。

- XAML 元素丢失结束标记。

- XAML 元素出现在不允许使用的位置。

有关常见 XAML 语法的详细信息，请参阅[基本 XAML 语法指南](/windows/uwp/xaml-platform/xaml-syntax-guide)。

你还可以在 Blend 中标识和解决简单的代码隐藏语法错误、编译错误和运行时错误。 但是，在 Visual Studio 中标识和解决代码隐藏错误会更加轻松。

### <a name="debugging-sample-xaml-code"></a>调试示例 XAML 代码

下面的示例将引导你在 Blend 中完成一个简单的 XAML 调试会话。

#### <a name="to-create-a-project"></a>创建项目

1. 在 Blend 中，打开 " **文件** " 菜单，然后单击 " **新建项目**"。

    在“新建项目”对话框中，左侧会显示项目类型列表****。 单击一种项目类型后，右侧将显示与该类型关联的项目模板。

2. 在项目类型列表中，单击 " **Windows 通用**"。

3. 在项目模板列表中，单击 " **空白应用" (通用 Windows) **。

4. 在“名称”文本框中，键入 `DebuggingSample`****。 

5. 在“位置”文字框中，验证项目的位置****。

6. 在“语言”中，单击“Visual C#”，然后单击“确定”创建项目************。

7. 在设计图面上右键单击，然后单击“查看源”，切换到“拆分”视图********。 

8. 通过单击代码右上角的“复制”链接复制以下代码****。

   ```xml
   <Grid HorizontalAlignment="Left" Height="222" VerticalAlignment="Top>
        <Button content="Button" x:Mame="Home" HorizontalAlignment="Left" VerticalAlignment="Top"/>
        <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="0,38,0,0">
        <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="0,75,0,0"/>
        <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="0,112,0,0"/>
        <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top Margin="0,149,0,0"/>
   </Grid>
   ```

9. 找到默认“网格”，将代码粘贴到起始和结束 Grid 标记之间********。 完成后，代码看起来应类似下面这样：

    ```xml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
         <Grid HorizontalAlignment="Left" Height="222" VerticalAlignment="Top>
              <Button content="Button" x:Mame="Home" HorizontalAlignment="Left" VerticalAlignment="Top"/>
              <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="0,38,0,0">
              <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="0,75,0,0"/>
              <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="0,112,0,0"/>
              <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top Margin="0,149,0,0"/>
         </Grid>
    </Grid>
    ```

10. 按**Ctrl** + **Shift** + **B**生成项目。

    将显示一条错误消息，表示无法生成该项目，并且应用的底部将显示列出了错误的“结果”面板****。

    ![在 Blend for Visual Studio 中调试 XAML](../debugger/media/blend_debugxaml_xaml.png "blend_debugXAML_XAML")

### <a name="resolve-xaml-errors"></a>解决 XAML 错误

检测到 XAML 错误后，设计图面会显示一条指示项目包含无效标记的警报。 纠正错误时，“结果”面板中的错误列表会进行更新****。 在纠正所有错误后，设计图面将启用，并且设计图面上将显示你的应用。

#### <a name="to-resolve-the-xaml-errors"></a>纠正 XAML 错误

1. 双击列表中的第一个错误。 此描述为“值 ‘<’ 在特性中无效”。 双击该错误时，指针会在代码中找到相应的位置。 `<` 前面的 `Button` 是有效的，但不是错误消息中建议的特性。 如果你查看上一个代码行，则会注意到特性 `Top` 的右引号缺失。 键入右引号。 “结果”面板中的错误列表会进行更新以反映更改****。

2. 双击描述“'0' 在名称的开头无效”。 `Margin="0,149,0,0"` 的格式似乎是正确的。 但请注意，`Margin` 的颜色编码与代码中的其他 `Margin` 实例不匹配。 由于前面的名称/值对 (`VerticalAlignment="Top`) 中缺少右引号，因此 `Margin="` 将作为前面的特性值的一部分读取，而 0 将作为名称/值对的开头读取。 为 `Top` 键入右引号。 “结果”面板中的错误列表会进行更新以反映更改****。

3. 双击剩余错误“结束 XML 标记‘Button’不匹配”。 指针位于“网格”**** 结束标记处 (`</Grid>`)，指示错误在 `Grid`对象内。 请注意，第二个 `Button` 对象缺少结束标记。 添加结束标记 `/` 后，“结果”**** 面板列表会进行更新。 现在已纠正这些初始错误，并且已标识另外两个错误。

4. 双击“无法识别或访问成员‘content’”。 `c` 中的 `content` 应为大写。 将小写“c”替换为大写“c”。

5. 双击 "命名空间中不存在属性 ' Mame '" `http://schemas.microsoft.com/winfx/2006/xaml` 。 “Mame”中的“M”应为“N”。 将“M”替换为“N”。 现在可以分析 XAML，应用程序将显示在设计图面上。

    ![在 Blend for Visual Studio 中调试 XAML](../debugger/media/blend_debugartboard_xaml.png "blend_debugArtboard_XAML")

    按**Ctrl** + **Shift** + **B**生成项目，并确认没有剩余错误。

## <a name="debug-in-visual-studio"></a>在 Visual Studio 中进行调试

您可以在 Visual Studio 中打开 Blend 项目，以便更轻松地在应用程序中调试代码。 若要在 Visual Studio 中打开 Blend 项目，请在 " **项目** " 面板中右键单击该项目，然后单击 " **在 Visual studio 中编辑**"。 在 Visual Studio 中完成调试会话后，按 Ctrl + Shift + S 保存所有更改，然后切换回 Blend。 系统将提示你重新加载该项目。 单击 **"是" 以** 继续在 Blend 中工作。

有关调试应用的详细信息，请参阅 [在 Visual Studio 中调试 UWP 应用](../debugger/debugging-windows-store-and-windows-universal-apps.md)。

## <a name="get-help"></a>获取帮助

如果需要更多帮助调试混合应用，可以在 [UWP 应用社区论坛](https://social.msdn.microsoft.com/Forums/windowsapps/home?category=windowsapps) 中搜索与问题相关的帖子或发布问题。
