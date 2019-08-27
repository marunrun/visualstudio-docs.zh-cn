---
title: 布局
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: c19e3022-047c-43b6-a046-a82717efed4f
caps.latest.revision: 3
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 09656b9afac82eec8981f8573af87391c99a3688
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68179771"
---
# <a name="layout-for-visual-studio"></a>Visual Studio 的布局
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Visual Studio 对话框大部分[实用程序对话框布局](../../extensibility/ux-guidelines/layout-for-visual-studio.md#BKMK_UtilityDialogLayout)，这是 unthemed 对话框该遵循标准[Windows Desktop 对话框布局原则](https://msdn.microsoft.com/library/windows/desktop/dn742499\(v=vs.85\).aspx)。 在 Visual Studio 移动以刷新其 UI 时，一些更加醒目的对话框具有建立它们为产品定义体验的新设计。 这些[主题对话框布局](../../extensibility/ux-guidelines/layout-for-visual-studio.md#BKMK_ThemedDialogLayout)具有主题化的外观。

## <a name="BKMK_UtilityDialogLayout"></a> 实用工具对话框布局

- 实用程序对话框中的所有控件应开始顶部/左侧，向下流动。

- 永远不会在一个对话框，以填充较大的区域上居中对齐控件。

- 使用环境字体的对话框中的所有文本。 在编写时 visual 规范，指定环境字体而不是选择特定的字体和大小。 请参阅[环境字体](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TheEnvironmentFont)。

- 使用一致的控制间距和放置以支持目标中耕耘所得到的质量。

- 对话框会变为可从更多控件、 控件、 唯一 juxtaposition 或这两者的更复杂。 有关这些复杂的情况下，允许控件分组为用户提供的逻辑流分析之间有足够的空间。

### <a name="utility-dialog-layout-examples"></a>实用工具对话框布局示例
 以像素为单位表示的所有维度。

 ![控件上方标签的对话框间距](../../extensibility/ux-guidelines/media/0801-a-utilityspacingabove.png "0801 a_UtilitySpacingAbove")

 **图 a: 08.01实用工具使用控件上方标签的对话框间距准则**

 ![控件左侧标签的对话框间距](../../extensibility/ux-guidelines/media/0801-b-utilityspacingleft.png "0801 b_UtilitySpacingLeft")

 **图 b: 08.01实用程序与控件左侧标签的对话框间距准则**

### <a name="layout-details"></a>布局的详细信息

#### <a name="margins"></a>边距

- 所有对话都应都具有所有边缘周围 12 像素的边框。

- 组范围内的边距应为从框架边缘的 9 个像素。

- 在选项卡控件内的边距应为 6 个像素从选项卡控件的边缘。

#### <a name="command-buttons"></a>命令按钮

- 在内容的对话框框架上运行的命令按钮。 它们应放置在底部右侧，并且应具有足够上述设置这些按钮分别单独的变量空间。

- 如果有运行在对话框中的水平按钮，备用命令按钮配置是在右上角的垂直堆栈。 请参阅[内部命令按钮](../../extensibility/ux-guidelines/layout-for-visual-studio.md#BKMK_InteriorCommandButtons)下面。

- 左侧的命令按钮 （底部左侧/中间位置对话框） 的空间是被视为"带区"对话框操作控件的一部分。 应起、 强行进入该空间的唯一事情是与整个任务或对话框的帮助链接。

- 命令按钮应为 75 x 23 像素。

- 命令按钮应为 6 个像素相隔。

  ![基本按钮对齐](../../extensibility/ux-guidelines/media/0801-c-buttonalign.png "0801 c_ButtonAlign")

  **图 08.01 c:基本按钮对齐方式**

#### <a name="labels"></a>标签

- 左对齐所有标签。

- 对于上一个控件的标签，它们应该左对齐精确地使用其下方的控件以及标签的底部应为 5 像素，上面的其他控件 （例如，组合框） 的顶部。

- 对于位于左侧的控件的标签，标签和输入的控件之间的最小宽度为 10 像素。 应为对齐的文本框、 组合框或其他控件建立的隐含的第二个列。

- 标签是句首大写后, 跟一个冒号。 请参阅[文本样式](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TextStyle)。

#### <a name="distance-between-controls"></a>控件之间的距离
 合理的堆栈控件。 堆积控件之间的间距没有绝对准则。 在控件之间拟合度可能对话框之间略有不同。 建议的间距是垂直的控制/标签对 20 像素和 9 像素水平控件/标签对。 水平对的最小控件间距是 6 个像素。

 ![建议的控件之间的距离](../../extensibility/ux-guidelines/media/0801-d-controldistance.png "0801 d_ControlDistance")

 **图 08.01-d:控件之间的距离的建议**

#### <a name="control-indentation"></a>控制缩进
 当控件被嵌套时，对齐水平方向，使用控件更高版本，通常是标签的左边缘的内部控件。

 ![嵌套的控件对齐效果](../../extensibility/ux-guidelines/media/0801-e-controlalign.png "0801 e_ControlAlign")

 **图 08.01 e:嵌套的控件对齐方式**

#### <a name="control-width"></a>控件宽度
 应不超过该字段的平均输入文本框或其他类似控件的宽度。 平均英语单词是五个字符。 例如，需要一个长路径名称的文本框中应是，只要允许水平布局，而下拉列表中的平台名称只应允许最长的项的长度。

#### <a name="helper-text"></a>帮助程序文本

- 一个对话框，可以显示提供了有关用途的对话框的详细信息的帮助程序文本。 这通常位于顶部，并可以是 1-2 的句子。

- 行长度应为用户分析和读取的适应宽度。 中等对话框应不超过 550 像素宽。

#### <a name="BKMK_InteriorCommandButtons"></a> 内部命令按钮
 更复杂的对话框中内部控件可能具有其自身相关的按钮，这可能会影响在对话框的提交按钮的位置。

- 使用内部为垂直对齐方式 （列） 按钮**确定**/**取消**水平方向，在右下角中。

- 使用内部为水平对齐方式 （行） 按钮**确定**/**取消**垂直方向，在右上角中。 这种情况下并不常见。

- 内部的按钮的大小应为目标的 75 x 23 像素，匹配的大小的标准按钮大小**确定**/**取消**按钮在可能的情况。 如果按钮标签超出标准按钮大小的按钮，在该集中其他按钮应与该更广的大小保持一致。

  ![水平确定和取消按钮](../../extensibility/ux-guidelines/media/0801-f-horizokcan.png "0801 f_HorizOKCan")

  **图 f: 08.01垂直内部水平确定 / 取消按钮**

  ![垂直确定和取消按钮](../../extensibility/ux-guidelines/media/0801-g-vertokcan.png "0801 g_VertOKCan")

  **图 g: 08.01水平内部垂直确定 / 取消按钮**

#### <a name="browse-button"></a>[浏览...]按钮
 **[浏览...]** 遵循文本框中的按钮应拼写成"浏览..."完整版包括省略号。 如果空间紧密或有多个 **[浏览...]** 屏幕按钮上的按钮可以减少到只需省略号。

## <a name="BKMK_ThemedDialogLayout"></a> 主题对话框布局
 在 Visual Studio 中的主题对话框具有较浅的外观和提供更多的空白空间。 版式提供更多强调和感兴趣，提供更多开放行距和字体大小和权重的一种变体。 在可能的情况下，chrome 和标题栏已减少或删除。 这些对话框的布局应遵循此基本模式：

1. 对话框的背景为白色。

2. 中的中间值灰色没有 1 像素规则边框。

3. 对话框标题不再位于标题栏，但提供了视觉吸引力和放在更大的点大小。 (请参阅中的字体大小部分[文本样式](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TextStyle)。)

4. 应结合其他文本，说明，例如标签**环境字体 + 粗体**。

5. 以浅灰色的 1 像素规则分隔内部的列。

6. 默认链接提供了不带下划线。 悬停和按下的状态已更改颜色以及下划线。

7. 提交按钮 (如**确定**/**取消**) 位于右下角。

### <a name="themed-dialog-layout-examples"></a>主题对话框布局示例
 ![主题对话框布局](../../extensibility/ux-guidelines/media/0801-h-themeddialog.png "0801 h_ThemedDialog")

 **图 08.01-h:主题对话框**

 ![主题对话框尺寸](../../extensibility/ux-guidelines/media/0801-i-themeddialogdimensions.png "0801 i_ThemedDialogDimensions")

 **图 08.01 实现：主题对话框 – 维度**

 ![主题对话框字体](../../extensibility/ux-guidelines/media/0801-j-themeddialogfonts.png "0801 j_ThemedDialogFonts")

 **图 j: 08.01主题对话框 – 字体**

 ![主题对话框颜色](../../extensibility/ux-guidelines/media/0801-k-themeddialogcolors.png "0801 k_ThemedDialogColors")

 **图 08.01-k:主题对话框 – 颜色**

## <a name="see-also"></a>请参阅
 [Visual Studio 的应用程序模式](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md)[控件 (Windows)](https://msdn.microsoft.com/library/windows/desktop/dn742399.aspx) [对话框 (Windows)](https://msdn.microsoft.com/library/windows/desktop/dn742499\(v=vs.85\).aspx)
