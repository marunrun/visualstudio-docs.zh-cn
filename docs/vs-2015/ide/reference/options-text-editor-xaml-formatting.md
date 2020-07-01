---
title: “选项”->“文本编辑器”->“XAML”->“格式设置”| Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.XAML.Formatting.General
- VS.ToolsOptionsPages.Text_Editor.XAML.Miscellaneous
- VS.ToolsOptionsPages.Text_Editor.XAML.Formatting.Spacing
helpviewer_keywords:
- element spacing, XAML view settings
- attribute spacing, XAML view settings
- XAML view settings, auto-formatting events
- auto-formatting events, XAML view settings
- XAML view settings, tag wrapping
- XAML view settings, auto insert
- quotation mark style, XAML view settings
- XAML formatting, WPF Designer
- XAML view settings, Toolbox
- XAML view settings, element spacing
- default view, XAML view settings
- auto insert, XAML view settings
- XAML view settings, default view
- XAML view settings, quotation mark style
- tag wrapping, XAML view settings
- WPF Designer, XAML formatting
- XAML view settings, attribute spacing
ms.assetid: ad3820b1-0d94-4807-a74c-c3467ed973a2
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 537223aab878aee2fb00e9417d0415f0a17d2dd5
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85534129"
---
# <a name="options-text-editor-xaml-formatting"></a>选项，文本编辑器，XAML，格式
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

使用“格式设置”  属性页可指定如何在 XAML 文档中设置元素和特性的格式。 若要打开“选项”  对话框，请单击“工具”  菜单，然后单击“选项”  。 若要访问“格式设置”**** 属性页，请依次展开“文本编辑器”****、“XAML”****、“格式设置”**** 节点。

> [!NOTE]
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。

## <a name="auto-formatting-events"></a>自动格式化事件
检测到以下任一事件时，可能引发自动格式设置。

- 完成结束标记或简单标记。

- 完成开始标记。

- 从剪贴板粘贴。

- 设置键盘命令格式。

  可以指定引发自动格式设置的事件。

|“属性”|描述|
|-|-|
|**结束标记或简单标记完成时**|完成键入结束标记或简单标记时引发自动格式设置。 简单标记没有特性，例如 `<Button />`。|
|**开始标记完成时**|完成键入开始标记时引发自动格式设置。|
|**从剪贴板粘贴时**|将 XAML 从剪贴板粘贴到 XAML 视图时引发自动格式设置。|

## <a name="quotation-mark-style"></a>引号样式
此设置指示特性值是括在单引号内，还是括在双引号内。 自动格式设置程序和 IntelliSense 自动完成功能都使用此设置。

设置此选项后，受影响的只有随后在 XAML 视图中使用设计器添加或手动添加的特性。

|“属性”|描述|
|-|-|
|**双引号 (")**|特性值括在双引号内。<br /><br /> `<Button Name="button1">Hello</Button>`|
|**单引号 (')**|特性值括在单引号内。<br /><br /> `<Button Name='button1'>Hello</Button>`|

## <a name="tag-wrapping"></a>标记换行
可以为标记换行指定一个行长度。 启用标记换行后，随后使用设计器添加的所有 XAML 将进行适当换行。

|“属性”|描述|
|-|-|
|**对超出指定长度的标记执行换行**|指定是否在“长度”**** 指定的行长度处换行。|
|**长度**|一行中可以包含的字符数。 如有必要，某些 XAML 行可以超过指定的行长度。|

## <a name="attribute-spacing"></a>特性间距
使用此设置可以控制特性在 XAML 文档中的排列方式

|“属性”|描述|
|-|-|
|**在特性之间保留换行符和空格**|特性之间的换行符和空格不受自动格式设置的影响。<br /><br /> `<Button Height="23" Name="button1"`<br /><br /> `Width="75">Hello</Button>`|
|**在特性之间插入单个空格**|特性占用一行，由一个空格分隔相邻的特性。 应用标记换行设置。<br /><br /> `<Button Height="23" Name="button1" Width="75">Hello</Button>`|
|**将各个特性分行放置**|每个特性单占一行。 当存在很多特性时，此设置非常有用。<br /><br /> `<Button`<br /><br /> `Height="23"`<br /><br /> `Name="button1"`<br /><br /> `Width="75">Hello</Button>`|
|**将第一个特性放在与开始标记相同的行上**|选中该项时，第一个特性与元素的开始标记显示在同一行上。<br /><br /> `<Button Height="23"`<br /><br /> `Name="button1"`<br /><br /> `Width="75">Hello</Button>`|

## <a name="element-spacing"></a>元素间距
使用此设置可以控制元素在 XAML 文档中的排列方式

|                                                               |                                                                                                                                                                                       |
|---------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **保留内容中的新行**                             | 不移除元素内容中的空行。<br /><br /> `<Grid>`<br /><br /><br /><br /><br /><br /> `<Button Name="button1">Hello</Button>`<br /><br /><br /><br /> `</Grid>\`   |
| **将内容中的多个空行折叠为单个行** | 元素内容中的多个空行会折叠为单个行。<br /><br /> `<Grid>`<br /><br /><br /><br /> `<Button Name="button1">Hello</Button>`<br /><br /><br /><br /> `</Grid>` |
| **移除内容中的空行**                             | 移除元素内容中的所有空行。<br /><br /> `<Grid>`<br /><br /> `<Button Name="button1">Hello</Button>`<br /><br /> `</Grid>`                                        |

## <a name="auto-insert"></a>自动插入
使用此设置可以控制自动生成标记和引号的时间。

|“属性”|描述|
|-|-|
|**结束标记**|指定使用大于号字符 (>) 关闭开始标记时，是否自动生成元素的结束标记。|
|**特性引号**|指定从语句完成下拉列表中选择特性值时，是否生成封闭引号。|
|**MarkupExtensions 的右大括号**|指定键入左括号字符 ({) 时，是否自动生成标记扩展的右括号 (})。|
|**用于分隔 MarkupExtension 参数的逗号**|指定在标记扩展中键入多个参数时是否生成逗号。|

## <a name="default-view"></a>默认视图
使用此设置来控制是否在加载 XAML 文档时显示设计视图。

|“属性”|描述|
|-|-|
|**始终在完整 XAML 视图中打开文档**|指定 XAML 文档是否仅出现在 XAML 视图中，无设计视图。 用于加载大型文档。|

## <a name="toolbox"></a>工具箱
使用此设置可指定是否在工具箱中显示用户控件和自定义控件。

|“属性”|描述|
|-|-|
|**自动填充工具箱项**|指定当前解决方案中的用户控件和自定义控件是否自动显示在工具箱中。|

## <a name="see-also"></a>另请参阅
WPF 中的[XAML](https://msdn.microsoft.com/library/5d858575-a83b-42df-ad3f-047ed2d6e3c8) 
[如何：更改 XAML 视图设置](https://msdn.microsoft.com/aee87c79-ca01-4f84-8fb7-a9e47048ee47) 
[XAML 和代码演练](https://msdn.microsoft.com/b3ff41a0-a2a3-4f61-b698-ac88ec8f799c)
