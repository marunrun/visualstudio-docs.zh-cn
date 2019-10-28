---
title: 折叠和展开代码区域
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- outlining
- Visual Studio, expand/collapse code
- Visual Studio, outlining
- expand/collapse code
- code [Visual Studio], outlining
- code [Visual Studio], hiding
- outlining code
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 791663c04d1c1e79eebaed39d339d8d118ffeaae
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72748855"
---
# <a name="outlining"></a>大纲显示

你可以选择隐藏视图中的某些代码，方法是折叠某个区域的代码，使其显示在加号 + 下面  。 单击加号可展开折叠的区域。 如果你使用的是键盘，则可选择使用 Ctrl+M+M 来进行折叠和展开    。 你还可以双击大纲边距（位于代码左侧）上的区域中的任意行来折叠大纲区域。 将鼠标悬停在折叠区域时，可以看见折叠区域的内容提示。

> [!NOTE]
> 本主题适用于 Visual Studio  Windows 版。 对于 Visual Studio for Mac，请参阅[源编辑器 (Visual Studio for Mac)](/visualstudio/mac/source-editor)。

将鼠标悬停在边距上时也会突出显示大纲边距中的区域。 在某些颜色配置中，默认的突出显示颜色可能看起来很模糊。 可在“工具” > “选项” > “环境” > “字体和颜色” > “可折叠区域”中更改此颜色      。

当处理以大纲方式显示的代码时，可以展开要处理的部分，完成后将其折叠，然后移到其他部分。 如果不希望使用大纲显示方式，可以使用**停止大纲显示**命令删除大纲信息，但是不会影响基础代码。

 “编辑”菜单上的“撤消”  和“重做”  命令会影响这些操作。 **复制**、**剪切**、**粘贴**和拖放操作可保留大纲信息，但是不保留可折叠区域的状态。 例如，如果复制处于折叠状态的区域，那么**粘贴**操作将把复制的文本作为展开的区域进行粘贴。

> [!CAUTION]
> 如果更改大纲显示区域，那么大纲显示可能失效。 例如，删除或“查找和替换”操作可能删除区域的结尾标记。

“编辑” > “大纲显示”子菜单包含以下命令   。

|||
|-|-|
|隐藏选定内容|（Ctrl+M、Ctrl+H）- 折叠所选的代码块，此功能通常不可用于大纲显示，例如 `if` 代码块     。 若要删除自定义区域，请使用“停止隐藏当前内容”（或使用 Ctrl+M、Ctrl+U）      。 此命令不可用于 Visual Basic。|
|切换大纲显示展开|- 当游标位于嵌套的折叠部分时，反转大纲最内层部分的当前的隐藏或展开状态。|
|切换所有大纲显示|（Ctrl+M、Ctrl+L）- 将所有区域设置为相同的折叠或展开状态     。 如果一些区域为展开状态，一些为折叠状态，那么将展开折叠区域。|
|停止大纲显示|（Ctrl+M、Ctrl+P）- 删除整个文档的所有大纲信息     。|
|停止隐藏当前内容|（Ctrl+M、Ctrl+U）- 删除当前所选的用户定义的区域的大纲信息     。 此命令不可用于 Visual Basic。|
|折叠到定义|（Ctrl+M、Ctrl+O）- 折叠所有类型的成员     。|
|折叠块：\<逻辑边界>|(C++) 折叠包含插入点的函数中的一个区域。 例如，如果插入点在一个循环内，则隐藏此循环。|
|全部折叠：\<逻辑结构>|(C++) 折叠函数内的所有结构。|

你还可以使用 Visual Studio SDK 定义想要展开或折叠的文本区域。 请参阅[演练：大纲显示](../extensibility/walkthrough-outlining.md)。

## <a name="see-also"></a>请参阅

- [代码编辑器功能](../ide/writing-code-in-the-code-and-text-editor.md)
- [源编辑器 (Visual Studio for Mac)](/visualstudio/mac/source-editor)