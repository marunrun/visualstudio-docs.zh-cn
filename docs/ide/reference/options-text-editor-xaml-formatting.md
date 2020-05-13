---
title: 选项，文本编辑器，XAML，格式
ms.date: 10/29/2018
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.XAML.Formatting.General
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
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- uwp
ms.openlocfilehash: d340a3b9468ea23c4cab23aabe19a7c1390955a3
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75568238"
---
# <a name="options-text-editor-xaml-formatting"></a>选项，文本编辑器，XAML，格式

使用“格式设置”  属性页可指定如何在 XAML 文档中设置元素和特性的格式。 若要打开“选项”  对话框，请单击“工具”  菜单，然后单击“选项”  。 要访问“格式设置”属性页，请展开“文本编辑器” **“XAML”** “格式设置”节点   >    >   。

## <a name="auto-formatting-events"></a>自动格式化事件

检测到以下任一事件时，可能引发自动格式设置。

- 完成结束标记或简单标记。

- 完成开始标记。

- 从剪贴板粘贴。

- 设置键盘命令格式。

可以指定引发自动格式设置的事件。

**结束标记或简单标记完成时**

完成键入结束标记或简单标记时引发自动格式设置。 简单标记没有特性，例如 `<Button />`。

**开始标记完成时**

完成键入开始标记时引发自动格式设置。

**从剪贴板粘贴时**

将 XAML 从剪贴板粘贴到 XAML 视图时引发自动格式设置。

## <a name="quotation-mark-style"></a>引号样式

此设置指示特性值是括在单引号内，还是括在双引号内。 自动格式设置程序和 IntelliSense 自动完成功能都使用此设置。

设置此选项后，受影响的只有随后在 XAML 视图中使用设计器添加或手动添加的特性。

**双引号 (")**

特性值括在双引号内。
`<Button Name="button1">Hello</Button>`

**单引号 (')**

特性值括在单引号内。
`<Button Name='button1'>Hello</Button>`

## <a name="tag-wrapping"></a>标记换行

可以为标记换行指定一个行长度。 启用标记换行后，随后使用设计器添加的所有 XAML 将进行适当换行。

**对超出指定长度的标记执行换行**

指定是否在“长度”  指定的行长度处换行。

**长度**

一行中可以包含的字符数。 如有必要，某些 XAML 行可以超过指定的行长度。

## <a name="attribute-spacing"></a>特性间距

使用此设置可以控制特性在 XAML 文档中的排列方式

**在特性之间保留换行符和空格**

特性之间的换行符和空格不受自动格式设置的影响。

```xml
<Button Height="23"   Name="button1"
Width="75">Hello</Button>
```

**在特性之间插入单个空格**

特性占用一行，由一个空格分隔相邻的特性。 应用标记换行设置。

```xml
<Button Height="23" Name="button1" Width="75">Hello</Button>
```

**将各个特性分行放置**

每个特性单占各自的行，这在存在许多特性很有用。

```xml
<Button
Height="23"
Name="button1"
Width="75">Hello</Button>
```

**将第一个特性放在与开始标记相同的行上**

选中该项时，第一个特性与元素的开始标记显示在同一行上。

```xml
<Button Height="23"
Name="button1"
Width="75">Hello</Button>
```

## <a name="element-spacing"></a>元素间距

使用此设置可以控制元素在 XAML 文档中的排列方式。

**保留内容中的新行**

不移除元素内容中的空行。

```xml
<Grid>

<Button Name="button1">Hello</Button>

</Grid>
```

**将内容中的多个空行折叠为单个行**

元素内容中的多个空行会折叠为单个行。

```xml
<Grid>

<Button Name="button1">Hello</Button>

</Grid>
```

**移除内容中的空行**

移除元素内容中的所有空行。

```xml
<Grid>
<Button Name="button1">Hello</Button>
</Grid>
```

## <a name="see-also"></a>另请参阅

- [WPF 中的 XAML](/dotnet/framework/wpf/advanced/xaml-in-wpf)
