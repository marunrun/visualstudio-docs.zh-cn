---
title: 依次转到文件、符号和行
ms.date: 08/14/2018
ms.topic: conceptual
helpviewer_keywords:
- code editor, go to
- code editor, go to line
- go to line
- go to
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bb39f1d395e48351aeacb587556224b0f86aac3e
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75593780"
---
# <a name="find-code-using-go-to-commands"></a>使用“转到”命令查找代码

Visual Studio 的“转到”命令可执行代码的重点搜索，有助于快速找到指定项  。 可以从简单统一的页面中转到特定的行、类型、符号、文件和成员。

## <a name="how-to-use-it"></a>使用方法

输入 | 函数
------------ | ---
**键盘** | 按 Ctrl  +T  或 Ctrl  +, 
**鼠标** | 选择“编辑” > “转到” > “转到全部”

代码编辑器的右上方会显示一个小窗口。

![“转到所有”窗口](media/go-to-all.png)

在文本框中键入内容时，文本框下的下拉列表中会显示结果。 若要转到某个元素，请在列表中选择它。

![“定位到”窗口](../ide/media/vside_navigatetowindow.png)

还可以输入一个问号 (?) 来获取更多帮助  。

![转到全部帮助](media/go-to-all-help.png)

## <a name="filtered-searches"></a>经过筛选的搜索

默认会在所有解决方案项中搜索指定项。 不过，可以在搜索词前面加上特定字符，将代码搜索范围缩小至具体元素类型。 还可以选择“转到”对话框工具栏上的按钮，快速更改搜索筛选器  。 更改类型筛选器的按钮位于左侧，而更改搜索范围的按钮则位于右侧。

![转到成员](../ide/media/vside_navigation_toolbar.png)

### <a name="filter-to-a-specific-type-of-code-element"></a>筛选到特定类型的码位元素

要缩小对特定类型的码位元素的搜索范围，可以在搜索框中指定一个前缀，也可以从以下五个筛选器图标中选择一个：

前缀 | 图标 | 快捷方式 | 说明
:-: | - | - | -
:| ![行图标](media/gotoall-line-icon.png) | Ctrl  +G  | 转到指定行号
f| ![文件图标](media/gotoall-files-icon.png) | Ctrl  +1  、Ctrl  +F  | 转到指定文件
r| ![“最近使用的文件”图标](media/gotoall-recent-files-icon.png) | **Ctrl**+**1** **Ctrl**+**R** | 转到最近访问的指定文件
t| ![类型图标](media/gotoall-types-icon.png) | Ctrl  +1  、Ctrl  +T  | 转到指定类型
m| ![成员图标](media/gotoall-members-icon.png) | Ctrl  +1  、Ctrl  +M  | 转到指定成员
\#| ![符号图标](media/gotoall-symbols-icon.png) | Ctrl  +1  、Ctrl  +S  | 转到指定符号

### <a name="filter-to-a-specific-location"></a>筛选到特定位置

要将搜索范围缩小到特定位置，请从这两个文档图标中选择一个：

图标 | 说明
---- | ---
![当前文档](media/gotoall_currentdocument.png) | 仅搜索当前文档
![外部文档](media/gotoall_external.png) | 除了项目/解决方案中的文档外还搜索外部文档

## <a name="camel-casing"></a>驼峰式大小写

如果在代码中使用[驼峰式大小写](https://en.wikipedia.org/wiki/Camel_case)，可以仅输入码位元素名称的大写字母，以更快地查找码位元素。 例如，如果代码中有 `CredentialViewModel` 类型，可以选择“类型”筛选器 (t)，然后在“转到”对话框中仅输入名称的大写字母 (`CVM`) 来缩小搜索范围。 如果代码名称很长，此功能就非常有用。

![转到窗口 - 使用大写字母进行搜索](../ide/media/vside_capitalsearch.png)

## <a name="settings"></a>设置

选择齿轮图标 ![齿轮图标](media/gotoall_gear.png) 允许更改此功能的作用方式：

设置 | 说明
------- | ---
使用预览选项卡 | 在 IDE 的预览选项卡中立即显示所选的项
显示详细信息 | 在窗口的文档注释中显示项目、文件、行和摘要信息
使窗口居中 | 将此窗口移动到代码编辑器的正上方而不是右上方

## <a name="see-also"></a>另请参阅

- [导航代码](../ide/navigating-code.md)
- [“转到行”对话框](../ide/reference/go-to-line.md)
- [转到定义和速览定义](../ide/go-to-and-peek-definition.md)
