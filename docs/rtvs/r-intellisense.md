---
title: 适用于 R 代码的 IntelliSense
description: 在键入 R 代码时，Visual Studio IntelliSense 将显示有关函数、对象成员、代码片段和补全内容的信息。
ms.date: 01/24/2018
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: jillfra
ms.workload:
- data-science
ms.openlocfilehash: 854f7d410e327ca92d0c5156d89bc21765e13cc7
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "62999108"
---
# <a name="intellisense"></a>IntelliSense

编写代码时，Visual Studio IntelliSense 能直观显示可调用函数、对象成员、函数参数和[代码片段](code-snippets-for-r.md)的相关信息。 它还会在你键入时显示可能的补全内容，并在按 Tab 或 Enter 键时进行补全（请参阅“高级”选项卡中的[“编辑器”选项](editing-r-code-in-visual-studio.md#editor-options)）    。 编辑器和[交互窗口](interactive-repl-for-r-in-visual-studio.md)都支持 IntelliSense。

![显示函数签名的 IntelliSense](media/intellisense-function-signature.png)

键入函数或其他语句时，IntelliSense 提供按输入的内容筛选的自动补全菜单（区分大小写）：

![IntelliSense 自动补全菜单](media/intellisense-auto-complete-menu.png)

按 Tab 键（或 Enter、空格键，具体取决于如何设置选项），在下拉列表中插入所选项    。 可通过箭头键更改选择。

IntelliSense 还为 R 对象的成员提供建议：

![为对象成员提供的 IntelliSense 建议](media/intellisense-auto-complete-r-objects.png)

按 Esc 消除所有菜单  。 按 Ctrl+空格键可以再次恢复   。

为函数调用键入左括号 `(` 会同时插入右括号 `)`，然后弹出签名帮助，如前面所示：

![函数的 IntelliSense 签名帮助](media/intellisense-function-signature.png)

同样，按 Esc 消除弹出框；按 Ctrl+Shift+空格键可再次出现函数签名     。

> [!Tip]
> 如果参数帮助不显示其包含的文本，请按住 Ctrl 以显示参数帮助文本  。

## <a name="intellisense-for-user-defined-functions-and-variables"></a>适用于用户定义的函数和变量的 IntelliSense

IntelliSense 适用于相同文件中用户定义的函数，包括名称参数补全：

![适用于用户定义函数的 IntelliSense](media/intellisense-same-file-functions.png)

![适用于用户定义函数的 IntelliSense 参数补全](media/intellisense-parameter-completion.png)

IntelliSense 还适用于相同文件和当前会话中的变量：

![IntelliSense 变量补全](media/intellisense-variable-completion.png)

> [!Note]
> 在交互窗口中，IntelliSense 仅考虑当前 R 会话中的名称，并忽略项目中的文件。

## <a name="code-suggestions"></a>代码建议

当边距中显示灯泡（称之为智能标记）时，表示 Visual Studio 提示存在可用于常用操作的快捷方式。 例如，将鼠标悬停在编辑器中含 `library` 语句的行上，即可看见灯泡。 选择灯泡会显示可用选项：

![编辑器中适用于 R 的智能标记](media/intellisense-smart-tags.png)
