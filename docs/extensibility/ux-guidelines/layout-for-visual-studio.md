---
title: Visual Studio 布局 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: c19e3022-047c-43b6-a046-a82717efed4f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1dfafa26b314c35f81e5caf9c433b1b630d916f4
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72747171"
---
# <a name="layout-for-visual-studio"></a>Visual Studio 布局
大多数 Visual Studio 对话框都是[实用工具对话框布局](../../extensibility/ux-guidelines/layout-for-visual-studio.md#BKMK_UtilityDialogLayout)，它是遵循标准[Windows 桌面对话框布局原则](/windows/desktop/uxguide/win-dialog-box)的 unthemed 对话框。 当 Visual Studio 移动以刷新其 UI 时，一些更突出的对话框会有一种新的设计，可将它们建立为产品定义经验。 这些[主题对话框布局](../../extensibility/ux-guidelines/layout-for-visual-studio.md#BKMK_ThemedDialogLayout)具有主题外观。

## <a name="BKMK_UtilityDialogLayout"></a>实用工具对话框布局

- 实用工具对话框内的所有控件都应从顶部/左侧开始，然后向下传递。

- 永远不要使控件在对话框上居中以填充大区域。

- 对所有对话框文本使用环境字体。 编写视觉规范时，请指定环境字体，而不是选择特定的字体和字号。 请参阅[环境字体](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TheEnvironmentFont)。

- 使用一致的控件间距和位置来支持追求中的质量目标。

- 对话框可能会变得更复杂，更多控件和/或控件的唯一 juxtaposition。 对于这些复杂的情况，请在控件分组之间留出足够的空间，以便为用户提供要分析的逻辑流。

### <a name="utility-dialog-layout-examples"></a>实用工具对话框布局示例
 所有维度都以像素表示。

 ![控件上方标签的对话框间距](../../extensibility/ux-guidelines/media/0801-a_utilityspacingabove.png "0801-a_UtilitySpacingAbove")

 **图 08.01-a：带标签的实用工具对话框的间距准则控件**

 ![控件左侧的标签的对话框间距](../../extensibility/ux-guidelines/media/0801-b_utilityspacingleft.png "0801-b_UtilitySpacingLeft")

 **图 08.01-b：具有控件左侧标签的实用工具对话框的间距准则**

### <a name="layout-details"></a>布局详细信息

#### <a name="margins"></a>边距

- 所有对话都应有一个12像素的边框环绕所有边缘。

- 组框中的边距应该与帧边缘的距离为9个像素。

- 选项卡控件中的边距应该与选项卡控件的边缘之间的间距为6个像素。

#### <a name="command-buttons"></a>命令按钮

- 命令按钮在对话框框架上操作，而不是在内容上操作。 它们应位于右下方，并且应具有足够的可变空间，以将按钮设置为区分分隔。

- 如果在对话框中操作有水平按钮，则替换命令按钮配置是右上方的垂直堆栈。 请参阅下面的[内部命令按钮](../../extensibility/ux-guidelines/layout-for-visual-studio.md#BKMK_InteriorCommandButtons)。

- 命令按钮左侧的空间（对话框的左下方/中心）被视为对话操作控件 "带区" 的一部分。 此空间的唯一应对强行进入是一个与总体任务或对话相关的帮助链接。

- 命令按钮应为75x23 像素。

- 命令按钮应该相隔6个像素。

  ![基本按钮对齐方式](../../extensibility/ux-guidelines/media/0801-c_buttonalign.png "0801-c_ButtonAlign")

  **图 08.01-c：基本按钮对齐方式**

#### <a name="labels"></a>标签

- 左对齐所有标签。

- 对于位于控件上方的标签，它们应与下面的控件精确对齐，并且标签的底部应为另一个控件（例如组合框）顶部上方的5像素。

- 对于位于控件左侧的标签，标签和输入控件之间的最小宽度为10像素。 应为对齐文本框、组合框或其他控件而建立隐含的第二列。

- 标签为句子大小写，后跟一个冒号。 请参阅[文本样式](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TextStyle)。

#### <a name="distance-between-controls"></a>控件之间的距离
 堆栈控件合理。 堆积控件之间的间距没有绝对指导原则。 控件之间的 tightness 在对话框之间可能略有不同。 对于垂直控件/标签对，建议的间距为20个像素; 对于水平控件/标签对，建议的间距为9个像素。 水平对的最小控件间距为6像素。

 ![控件之间的建议距离](../../extensibility/ux-guidelines/media/0801-d_controldistance.png "0801-d_ControlDistance")

 **图 08.01-d：有关控件间距离的建议**

#### <a name="control-indentation"></a>控件缩进
 嵌套控件时，将内部控件与上面控件的左边缘水平对齐，通常是标签。

 ![嵌套控件对齐方式](../../extensibility/ux-guidelines/media/0801-e_controlalign.png "0801-e_ControlAlign")

 **图 08.01-e：嵌套控件对齐方式**

#### <a name="control-width"></a>控件宽度
 文本框或其他类似控件的宽度应该不超过字段的平均输入。 普通英语单词为五个字符。 例如，需要长路径名称的文本框应使用水平布局，而平台名称的下拉列表只应为允许最长条目的长度。

#### <a name="helper-text"></a>帮助器文本

- 对话框可以显示提供有关对话框用途的详细信息的帮助程序文本。 这通常位于顶部，可以是1-2 句子。

- 行长度应该是用户要分析和读取的舒适宽度。 中型对话的宽度不应超过550像素。

#### <a name="BKMK_InteriorCommandButtons"></a>内部命令按钮
 在更复杂的对话框中，内部控件可能有自己的相关按钮，这可能会影响对话框的提交按钮所在的位置。

- 当 **"确定" / "** **取消**" 在右下角水平方向上时，使用内部按钮的垂直对齐方式（列）。

- 当 **"确定" / "** **取消**" 在右上角垂直方向时，使用内部按钮的水平对齐方式（行）。 这种情况不太常见。

- 内部按钮大小应以75x23 像素的标准按钮大小为目标，如果可能，匹配 **"确定" / "** **取消**" 按钮的大小。 如果按钮标签使按钮超过标准按钮大小，则该集合中的其他按钮应该与更大的大小一致。

  ![水平 "确定" 和 "取消" 按钮](../../extensibility/ux-guidelines/media/0801-f_horizokcan.png "0801-f_HorizOKCan")

  **图 08.01-f：水平 "确定"/"取消" 的垂直内部按钮**

  ![垂直 "确定" 和 "取消" 按钮](../../extensibility/ux-guidelines/media/0801-g_vertokcan.png "0801-g_VertOKCan")

  **图 08.01-g：水平的内部按钮，垂直 "确定"/"取消"**

#### <a name="browse-button"></a>[浏览 ...]鼠标
 **[浏览 ...]** 文本框后面的按钮应拼写为 "浏览 ..."完整，包括省略号。 如果空间已紧密型，或者屏幕上有多个 "**浏览 ...** " 按钮，则可以将该按钮缩小为仅显示省略号。

## <a name="BKMK_ThemedDialogLayout"></a>主题对话框布局
 Visual Studio 中的主题对话框具有较浅的外观，并提供更多空白。 版式提供更多的强调和兴趣，提供更多的开放行距和字体大小和粗细的变化形式。 如果可能，则会减少或删除 chrome 和 title 栏。 这些对话的布局应遵循以下基本模式：

1. 该对话框的背景为白色。

2. 中间值灰色有一个1像素的规则边框。

3. 对话框标题不再位于标题栏中，但可提供视觉对象并强调更大的点大小。 （请参见[文本样式](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TextStyle)中的字号部分。）

4. 与其他文本耦合的标签（如说明）应为**环境字体 + 粗体**。

5. 内部列以浅灰色的1像素规则分隔。

6. 默认链接没有下划线。 悬停状态和按下状态具有颜色更改和下划线。

7. 右下角的提交按钮（如 **"确定" / "** **取消**"）。

### <a name="themed-dialog-layout-examples"></a>主题对话框布局示例
 ![主题对话框布局](../../extensibility/ux-guidelines/media/0801-h_themeddialog.png "0801-h_ThemedDialog")

 **图 08.01-h：主题对话框**

 ![主题对话框维度](../../extensibility/ux-guidelines/media/0801-i_themeddialogdimensions.png "0801-i_ThemedDialogDimensions")

 **图 08.01-i：主题对话框-维度**

 ![主题对话框字体](../../extensibility/ux-guidelines/media/0801-j_themeddialogfonts.png "0801-j_ThemedDialogFonts")

 **图 08.01-j：主题对话框-字体**

 ![主题对话框颜色](../../extensibility/ux-guidelines/media/0801-k_themeddialogcolors.png "0801-k_ThemedDialogColors")

 **图 08.01-k：主题对话框-颜色**

## <a name="see-also"></a>请参阅
- [Visual Studio 的应用程序模式](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md)
- [控件（Windows）](/windows/desktop/uxguide/controls)
- [对话框（Windows）](/windows/desktop/uxguide/win-dialog-box)