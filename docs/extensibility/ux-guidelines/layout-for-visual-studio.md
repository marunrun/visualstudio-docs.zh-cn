---
title: 视觉工作室的布局 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: c19e3022-047c-43b6-a046-a82717efed4f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4eb8eb7468751d46b922c15530389c554a8d3e36
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80698395"
---
# <a name="layout-for-visual-studio"></a>Visual Studio 的布局
大多数可视化工作室对话框是[实用程序对话框布局](../../extensibility/ux-guidelines/layout-for-visual-studio.md#BKMK_UtilityDialogLayout)，这是遵循标准[Windows 桌面对话框布局原则](/windows/desktop/uxguide/win-dialog-box)的无主题对话框。 当 Visual Studio 开始刷新其 UI 时，一些比较突出的对话框具有新的设计，可将其确立为产品定义体验。 这些[主题对话框布局](../../extensibility/ux-guidelines/layout-for-visual-studio.md#BKMK_ThemedDialogLayout)具有主题外观。

## <a name="utility-dialog-layout"></a><a name="BKMK_UtilityDialogLayout"></a>实用程序对话框布局

- 实用程序对话框中的所有控件都应从顶部 / 左侧开始并向动。

- 切勿将控件居中以填充大面积。

- 对所有对话框文本使用环境字体。 编写可视化规范时，请指定环境字体，而不是选择特定的字体和大小。 请参阅[环境字体](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TheEnvironmentFont)。

- 使用一致的控制间距和放置来支持工艺质量的目标。

- 从大量控件、控件的唯一并列或两者同时，对话框可能会变得更加复杂。 对于这些复杂情况，在控制分组之间留出足够的空间，为用户提供要分析的逻辑流。

### <a name="utility-dialog-layout-examples"></a>实用程序对话框布局示例
 所有尺寸均以像素表示。

 ![控件上方标签的对话框间距](../../extensibility/ux-guidelines/media/0801-a_utilityspacingabove.png "0801-a_UtilitySpacingAbove")

 **图 08.01-a：具有上方控件标签的实用程序对话框的间距指南**

 ![控件左侧标签的对话框间距](../../extensibility/ux-guidelines/media/0801-b_utilityspacingleft.png "0801-b_UtilitySpacingLeft")

 **图 08.01-b：控件左侧带有标签的实用程序对话框间距指南**

### <a name="layout-details"></a>布局详细信息

#### <a name="margins"></a>边距

- 所有对话框都应在所有边上具有 12 像素的边框。

- 组帧中的边距应为距帧边缘的 9 像素。

- 选项卡控件中的边距应为距选项卡控件边缘的 6 像素。

#### <a name="command-buttons"></a>命令按钮

- 命令按钮在对话框框架上操作，而不是在内容上操作。 它们应放置在右下角，并且应具有足够的可变空间，以便将按钮设置为明显分开。

- 如果对话框中存在操作的水平按钮，则备用命令按钮配置是右上角的垂直堆栈。 请参阅下面的[内部命令按钮](../../extensibility/ux-guidelines/layout-for-visual-studio.md#BKMK_InteriorCommandButtons)。

- 命令按钮左侧的空间（对话框的左下/居中）被视为对话框操作控件"波段"的一部分。 唯一应该侵入该空间的是与整个任务或对话框相关的帮助链接。

- 命令按钮应为 75x23 像素。

- 命令按钮应相距 6 像素。

  ![基本按钮对齐方式](../../extensibility/ux-guidelines/media/0801-c_buttonalign.png "0801-c_ButtonAlign")

  **图 08.01-c：基本按钮对齐**

#### <a name="labels"></a>标签

- 左对齐所有标签。

- 对于控件上方的标签，它们应与控件下方的控件精确对齐，标签底部应高于其他控件顶部 5 像素（例如，组合框）。

- 对于位于控件左侧的标签，标签和输入控件之间的最小宽度为 10 像素。 应建立用于对齐文本框、组合框或其他控件的隐含第二列。

- 标签是句子大小写，后跟冒号。 请参阅[文本样式](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TextStyle)。

#### <a name="distance-between-controls"></a>控件之间的距离
 堆叠控件合理。 堆叠控件之间的间距没有绝对准则。 控件之间的紧密性可能因对话框而异。 垂直控制/标签对的建议间距为 20 像素，水平控制/标签对为 9 像素。 水平对的最小控制间距为 6 像素。

 ![控件之间的建议距离](../../extensibility/ux-guidelines/media/0801-d_controldistance.png "0801-d_ControlDistance")

 **图 08.01-d：控件之间的距离建议**

#### <a name="control-indentation"></a>控制缩进
 嵌套控件时，将内部控件与上面控件的左边缘（通常是标签）水平对齐。

 ![嵌套控件对齐方式](../../extensibility/ux-guidelines/media/0801-e_controlalign.png "0801-e_ControlAlign")

 **图 08.01-e：嵌套控制对齐**

#### <a name="control-width"></a>控制宽度
 文本框或其他类似控件的宽度不应超过字段的平均输入。 平均英语单词是五个字符。 例如，需要长路径名称的文本框应为水平布局允许的时间，而平台名称的下拉列表应仅应为允许最长条目的长度。

#### <a name="helper-text"></a>帮助者文本

- 对话框可以显示帮助器文本，该文本提供有关对话框用途的详细信息。 这通常位于顶部，可以是 1-2 个句子。

- 线长应为用户解析和读取的舒适宽度。 中等对话框的宽度不应超过 550 像素。

#### <a name="interior-command-buttons"></a><a name="BKMK_InteriorCommandButtons"></a>内部命令按钮
 在更复杂的对话框中，内部控制可能具有其自己的相关按钮，这可能会影响对话框的提交按钮的位置。

- 当 **"确定**/**取消"** 在右下角水平方向时，使用内部按钮的垂直对齐（列）。

- 当 **"确定**/**取消"** 在右上角垂直定向时，使用内部按钮的水平对齐（行）。 这种情况不太常见。

- 内部按钮大小应针对 75x23 像素的标准按钮大小，尽可能匹配**OK**/**取消**按钮的大小。 如果按钮标签使按钮超过标准按钮大小，则该集中的其他按钮应与该较宽的大小对齐。

  ![水平“确定”和“取消”按钮](../../extensibility/ux-guidelines/media/0801-f_horizokcan.png "0801-f_HorizOKCan")

  **图 08.01-f：具有水平 OK/取消的垂直内部按钮**

  ![垂直“确定”和“取消”按钮](../../extensibility/ux-guidelines/media/0801-g_vertokcan.png "0801-g_VertOKCan")

  **图 08.01-g：具有垂直 OK/取消水平内部按钮**

#### <a name="browse-button"></a>[浏览...]按钮
 **[浏览...]** 文本框后按钮应拼写出"浏览..."完整，包括省略号。 如果空间很紧或屏幕上有多个 **[Browse...]** 按钮，则可以将按钮减少到仅省略号。

## <a name="themed-dialog-layout"></a><a name="BKMK_ThemedDialogLayout"></a>主题对话框布局
 Visual Studio 中的主题对话框外观更轻，并提供更多的空白。 排版提供了更多的强调和兴趣，提供了更多的开放线间距和字体大小和权重的变化。 在可能的情况下，铬和标题条已减少或删除。 这些对话框的布局应遵循以下基本模式：

1. 对话框的背景为白色。

2. 中间值灰色中有一个 1 像素规则边框。

3. 对话框标题不再位于标题栏中，而是以较大的点大小提供视觉兴趣和强调。 （请参阅[文本样式](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TextStyle)中的字体大小部分。

4. 与附加文本（如说明）加上的标签应为 **"环境"字体 = 粗体**。

5. 内部列由浅灰色 1 像素规则分隔。

6. 默认链接没有下划线。 悬停和按下状态的颜色变化加下划线。

7. 提交按钮（如**OK**/**取消**）位于右下角。

### <a name="themed-dialog-layout-examples"></a>主题对话框布局示例
 ![主题对话框布局](../../extensibility/ux-guidelines/media/0801-h_themeddialog.png "0801-h_ThemedDialog")

 **图 08.01-h：主题对话框**

 ![主题对话框尺寸](../../extensibility/ux-guidelines/media/0801-i_themeddialogdimensions.png "0801-i_ThemedDialogDimensions")

 **图 08.01-i：主题对话框 - 尺寸**

 ![主题对话框字体](../../extensibility/ux-guidelines/media/0801-j_themeddialogfonts.png "0801-j_ThemedDialogFonts")

 **图 08.01-j：主题对话框 - 字体**

 ![主题对话框颜色](../../extensibility/ux-guidelines/media/0801-k_themeddialogcolors.png "0801-k_ThemedDialogColors")

 **图 08.01-k：主题对话框 - 颜色**

## <a name="see-also"></a>请参阅
- [Visual Studio 的应用程序模式](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md)
- [控件（窗口）](/windows/desktop/uxguide/controls)
- [对话框（窗口）](/windows/desktop/uxguide/win-dialog-box)
