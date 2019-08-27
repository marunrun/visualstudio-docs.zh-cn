---
title: “选项”对话框 ->“环境”->“查找和替换”
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Environment.FindReplace
- VS.ToolsOptionsPages.Environment.FindandReplace
helpviewer_keywords:
- Find and Replace, Options dialog box
- Find and Replace, customizing
ms.assetid: f804d6d5-6309-46e4-8294-b83e880b5ec9
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7bc2d1a97676416c040c11c3b55f5adef7a0a3cc
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62790630"
---
# <a name="find-and-replace-environment-options-dialog-box"></a>“选项”对话框 ->“环境”->“查找和替换”

使用“选项”对话框的此页，可以控制消息框及查找和替换操作的其他方面。 单击“选项”，扩展“环境”，然后单击“查找和替换”，即可从“工具”菜单访问此对话框。 如果此页未出现在列表中，请在“选项”对话框中选择“显示所有设置”。

## <a name="uielement-list"></a>UIElement 列表

显示信息性消息

选择此选项可以显示所有具有“始终显示此消息”选项的“查找和替换”信息性消息。 例如，如果选择不显示消息“查找已到达搜索的起始点”，则选择此选项将导致此信息性消息在使用“查找和替换”时再次出现。

如果不想看到“查找和替换”的任何信息性消息，请清除此选项。

如果对某些“查找和替换”信息性消息（但不是全部）清除“始终显示此消息”选项，“显示信息性消息”复选框将被填充，但不会被选中。 若要还原所有可选的“查找和替换”消息，请先清除此选项，然后再次选择。

> [!NOTE]
> 此选项不会影响任何未显示“始终显示此消息”选项的“查找和替换”信息性消息。

显示警告消息

选择此选项可以显示所有具有“始终显示此消息”选项的“查找和替换”警告消息。 例如，如果选择不显示“全部替换”警告消息，而此消息又在你尝试在当前未打开进行编辑的文件中进行替换时出现，则选择此选项将导致此警告消息在你尝试全部替换时再次显示。

如果不想看到“查找和替换”的任何警告消息，请清除此选项。

如果对某些“查找和替换”警告消息（但不是全部）清除“始终显示此消息”选项，“显示警告消息”复选框将被填充，但不会被选中。 若要还原所有可选的“查找和替换”消息，请先清除此选项，然后再次选择。

> [!NOTE]
> 此选项不会影响任何未显示“始终显示此消息”选项的“查找和替换”警告消息。

使用编辑器中的文本自动填充“查找内容”

如果选择此选项，从“编辑”菜单选择“查找和替换”窗口的任何视图时，可以将当前编辑器插入点任何一侧的文本粘贴到“查找内容”字段。 清除此选项可以将上次搜索的最后一个搜索模式用作“查找内容”字符串。

## <a name="see-also"></a>请参阅

- [查找和替换文本](../../ide/finding-and-replacing-text.md)