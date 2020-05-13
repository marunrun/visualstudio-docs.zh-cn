---
title: R 的帮助窗口
description: 在 Visual Studio 中，R 的相关帮助通过 ? 命令直接集成到交互 对话框。
ms.date: 01/24/2018
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: jillfra
ms.workload:
- data-science
ms.openlocfilehash: af6c6156b1d88c1d015f7700fc7bed061bbe9a76
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "62950609"
---
# <a name="help-in-r-tools-for-visual-studio"></a>针对 Visual Studio 的 R 工具中的帮助

在 Visual Studio 中，R 的相关帮助直接集成到交互窗口中。 每当使用 `?` 命令（如`?mtcars`）时，Visual Studio 窗口中都会显示 R 文档提供的帮助：

![Visual Studio 中的帮助窗口](media/help-window.png)

> [!Tip]
> 与 Visual Studio 中的所有其他窗口一样，可按照任意喜欢的方式排列和停靠帮助窗口。 请参阅[在 Visual Studio 中自定义窗口布局](../ide/customizing-window-layouts-in-visual-studio.md)。
>
> 要在浏览器中打开帮助结果，请选择“R 工具” > “选项”菜单，并将“R 帮助浏览器”属性设置为 `External`    。 请参阅[选项](options-for-r-tools-in-visual-studio.md)。

若要搜索帮助，请使用 `??` 命令后跟搜索词的形式进行搜索。 如果搜索词包含空格，请使用引号：

```R
??"Motor Trend"
```

![帮助搜索结果](media/help-search1.png)

帮助窗口还包括一个搜索输入字段，可通过该字段直接在 R 文档中进行进一步搜索：

![使用输入字段的帮助搜索结果](media/help-search2.png)

## <a name="integrated-help-lookup"></a>集成帮助查找

开发人员通常搜索 R 文档寻找关于函数名称、数据集和其他元素的帮助。 针对 Visual Studio 的 R 工具 (RTVS) 将帮助查找直接集成到编辑器和交互式窗口，从而简化了该过程。

- 如果在自动完成操作期间按 F1，将生成一个列表，列出与子字符串匹配的帮助结果  。
- 右键单击搜索词（如某个函数），然后选择“相关帮助”命令即可打开该函数的帮助  。 还可对任何选定内容调用“相关帮助”  。

    ![通过右键单击上下文菜单调用帮助](media/help-right-click.png)

> [!Tip]
> 若要在浏览器中打开集成帮助，请选择“R 工具” > “选项”，并将“F1 Web 浏览器”设置为 `External`    。 请参阅[选项](options-for-r-tools-in-visual-studio.md)。

## <a name="integrated-stackoverflow-search"></a>集成的 StackOverflow 搜索

除了在 R 文档中搜索外，开发人员在编写代码时还经常搜索 StackOverflow。 RTVS 也简化了该过程。 右键单击某个词或所选内容，选择“Search web for”命令 (Ctrl+F1)，Visual Studio 将打开一个窗口，其中搜索结果的作用域为 StackOverflow    ：

![Visual Studio 中的 Web 搜索结果](media/help-web-search-results.png)

可通过“R 工具” > “选项” > “F1 Web 搜索字符串”选项更改追加的作用域字符串 `R site:stackoverflow`    ：

![更改 F1 Web 搜索字符串选项](media/options-dialog.png)

若要在浏览器中显示结果，则按[选项](options-for-r-tools-in-visual-studio.md)中所述，更改“F1 Web 浏览器”选项  。