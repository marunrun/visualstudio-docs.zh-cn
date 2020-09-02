---
title: 代码段
description: 如何使用代码片段在 Visual Studio for Mac 中高效编程
author: heiligerdankgesang
ms.author: dominicn
ms.date: 02/07/2019
ms.assetid: 0FE27C0C-A861-4133-A74E-8D0505CF5342
ms.openlocfilehash: 96344b72dd27095f8b9060078112fb767b1338fc
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "74984806"
---
# <a name="code-snippets"></a>代码片段

代码片段通常被称为“代码模板”，对高效编程很有帮助，因为它们支持插入和编辑预编写的代码块。 使用代码片段，可以方便地快速添加常用模式，甚至还可在使用不熟悉的语法进行开发时非常方便地学习新模式。 针对 C#、F#、HTML、XML、Python 和 Razor 提供了模板。

本部分介绍如何在代码中创建、插入和使用代码片段。

## <a name="inserting-a-snippet"></a>插入代码片段

可通过不同的方法添加代码片段，下面介绍了其中一些方法：

- **Tab 展开** &ndash; 开始键入模板名称，从列表中选择它，再按 Tab 两次来添加它：

  ![代码中的 Tab 展开](media/source-editor-image13.png)

- **工具箱** &ndash; 使用工具箱面板显示所有代码片段列表。 将任意模板从工具箱拖动到源代码中的正确位置：

  [![工具箱中的代码片段](media/source-editor-image14-sml.png)](media/source-editor-image14.png#lightbox)

- **插入模板命令** &ndash; 目前没有为插入模板设置默认的键绑定。 要创建一个键绑定，请浏览到“Visual Studio”>“首选项”>“键绑定”，并搜索 `template`。 这会将所需键绑定添加到“编辑绑定”字段中，然后单击“应用”：

  ![插入模板命令](media/source-editor-image15.png)

## <a name="creating-a-new-template"></a>创建新模板

虽然有多种语言的许多模板可供使用和编辑，但也可通过导航到“Visual Studio”>“首选项”>“文本编辑器”>“代码片段”来添加新模板：

![插入新模板](media/source-editor-image12.png)

按“添加”或“编辑”按钮创建或编辑代码片段。

## <a name="keywords-in-code-snippets"></a>代码片段中的关键字

将代码片段插入到编辑器之后，将突出显示任何定义的关键字，并可以通过在它们之间按 tab 键进行编辑。 关键字的行为类似于代码片段中的“变量”，通过在关键字名称前后放置一个美元符号 `$` 来对关键字进行定义。 

“编辑模板”窗口如下所示，编辑内置的 `prop` 片段。 片段包含两个关键字 &ndash; `$type$` 和 `$name$`，可在窗口右侧设置更多属性（如默认值和工具提示）：

![“编辑模板”窗口](media/source-editor-image12z.png)

以下字段用于定义一个片段：

- **快捷方式** &ndash; 用户为插入片段而键入的文本。
- **组合** &ndash; 使用此值将片段组合在片段内容菜单中。
- **说明** &ndash; 解释片段的用途。
- **Mime** &ndash; 控制片段适用于的文件类型。
- **是可展开的模板** &ndash; 确保选中此选项，以便可通过键入快捷方式在光标处插入片段。
- **使用模板括起来** &ndash; 选中此选项，在编辑器的“使用以下项括起来…”内容菜单中列出此快捷方式。
- **模板文本** &ndash; 将要插入到编辑器中的实际片段。 关键字占位符可以通过用美元符号等将令牌括起来进行定义。 `$type$`。
- **关键字属性面板** &ndash; 在右侧窗口中，使用顶部下拉列表选择一个关键字（例如 `type`）并编辑属性，如默认值和工具提示。

## <a name="using-keywords-in-the-editor"></a>在编辑器中使用关键字

若要使用带有关键字的片段（如上面定义的关键字），请键入快捷方式并按 Tab 两次，会将片段内容插入光标：

![插入的显示关键字的片段](media/source-editor-image12a.png)

按 Tab 键在 `object` 和 `MyProperty` 之间移动，以自定义类的片段。

关键字可以在片段中重复，如 `for` 示例所示，你会发现 `$i$` 关键字出现了 3 次：

![具有重复关键字的片段模板](media/source-editor-image12b.png)

在编辑器中使用时，Tab 键将在第一个 `i` 和 `max` 之间进行切换。 如果使用不同的变量名称改写 `i`，将更新所有三个实例：

![插入的显示多个关键字的片段](media/source-editor-image12c.png)

### <a name="reserved-keywords"></a>保留的关键字

有两个可以在片段中使用的保留的关键字：

- `$selected$` &ndash; 如果片段选中了“使用模板括起来”，则会将此关键字替换为在选择片段时在编辑器中突出显示的文本。
- `$end$` &ndash; 当用户完成编辑片段中的关键字时，光标将置于 `$end$` 关键字的位置。

上一部分中的 `for` 片段示范了这两个保留的关键字。

有关详细信息，请参阅 [Visual Studio 代码片段参考](/visualstudio/ide/code-snippets-schema-reference#keywords)。

## <a name="see-also"></a>另请参阅

- [代码片段（Windows 上的 Visual Studio）](/visualstudio/ide/code-snippets)