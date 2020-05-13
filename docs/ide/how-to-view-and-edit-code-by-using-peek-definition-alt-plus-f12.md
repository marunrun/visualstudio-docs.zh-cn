---
title: 使用查看定义
ms.date: 01/10/2018
ms.topic: conceptual
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9eac5c8c47c208f39f74f542fbbff89c8340a93f
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75591341"
---
# <a name="how-to-view-and-edit-code-by-using-peek-definition-altf12"></a>如何：使用“查看定义”查看和编辑代码 (Alt+F12)

可使用“查看定义”命令来查看和编辑代码，而无需离开正在编写的代码  。 “查看定义”和“转到定义”显示相同的信息，但“查看定义”在弹出窗口中显示，而“转到定义”在单独的代码窗口中显示代码     。 “转到定义”将导致上下文（即活动的代码窗口、当前行和光标位置）切换到定义代码窗口  。 使用“速览定义”时，无需离开原始代码文件就能查看和编辑定义，还能在定义文件内部到处移动  。

可对 C#、Visual Basic 和 C++ 代码使用“查看定义”  。 在 Visual Basic 中，“查看定义”显示一个链接，指向不包含定义元数据（例如内置的 .NET 类型）的符号的“对象浏览器”   。

## <a name="use-peek-definition"></a>使用“查看定义”

### <a name="open-a-peek-definition-window"></a>打开“查看定义”窗口

1. 若要速览定义，可以在右键单击菜单中对要浏览的类型或成员选择“速览定义”  。 如果启用该选项，还可以按“Ctrl”（或另一个修饰符）并单击成员名称来使用鼠标快速查看定义  。 或者在键盘上按 Alt  +F12  。

     本插图显示了名为  **的方法的“查看定义”窗口**`Print()`：

     ![“查看”窗口](../ide/media/peekwindow.png)

     定义窗口显示在原始文件的 `printer.Print("Hello World!")` 行的下方。 该窗口不会隐藏原始文件中的任何代码。 跟在 `printer.Print("Hello World!")` 后的行显示在定义窗口下。

1. 可将光标移动到查看定义窗口中的不同位置。 也可以在原始代码窗口中移动。

1. 可从定义窗口中复制字符串，并将其粘贴在原始代码中。 也可将字符串从定义窗口拖放到原始代码中，而不从定义窗口中删除它。

1. 可以选择 Esc 键或定义窗口选项卡上的“关闭”按钮来关闭定义窗口   。

### <a name="open-a-peek-definition-window-from-within-a-peek-definition-window"></a>从“查看定义”窗口内部打开一个“查看定义”窗口

如果“查看定义”窗口已打开，则可以对该窗口中的代码再次调用“查看定义”   。 此时将打开另一个定义窗口。 一组痕迹点将显示在定义窗口选项卡旁边，可用于在定义窗口之间导航。 每个点上的工具提示显示该点表示的定义文件的文件名和路径。

   ![“查看”窗口中的“查看”窗口](../ide/media/peekwithinpeek.png)

### <a name="peek-definition-with-multiple-results"></a>具有多个结果的“查看定义”

如果对具有多个定义的代码（例如，分部类）使用“查看定义”  ，则代码定义视图的右侧将显示结果列表。 你可选择列表中的任意结果来显示其定义。

   ![来自多个结果的“查看”窗口](../ide/media/peekmultiple.png)

### <a name="edit-inside-the-peek-definition-window"></a>在“查看定义”窗口中编辑

开始在“速览定义”窗口中编辑时，所修改的文件将在代码编辑器中作为单独的选项卡自动打开，并显示已完成的更改  。 可在“查看定义”窗口中继续更改、撤消更改和保存更改，该选项卡将继续显示这些更改  。 即使关闭“速览定义”窗口时没有保存更改，也可以在“速览定义”窗口中上次离开的位置继续在选项卡中更改、撤消更改和保存更多更改   。

   ![在“查看”窗口中编辑](../ide/media/peekedit.png)

### <a name="to-change-options-for-peek-definition"></a>更改速览定义的选项

1. 转到“工具”   > “选项”   > “文本编辑器”   > “常规”  。

1. 选择“在速览视图中打开定义”选项  。

1. 单击“确定”关闭“选项”对话框   。

   ![设置鼠标单击速览定义选项](../ide/media/editor_options_peek_view.png)

### <a name="keyboard-shortcuts-for-peek-definition"></a>“查看定义”的键盘快捷键

可在“查看定义”窗口中使用下列键盘快捷方式  ：

|功能|键盘快捷方式|
|-------------------|:-----------------------:|
|打开定义窗口|Alt**F12**+ |
|关闭定义窗口|Esc |
|将定义窗口提升为一个常规文档选项卡|Shift**Alt**Home+  + |
|在定义窗口间导航|**Ctrl**+**Alt**+ **-** 和 **Ctrl**+**Alt**+ **=**|
|在多个结果间导航|**F8** 和 **Shift**+**F8**|
|在代码编辑器窗口和定义窗口之间切换|Shift**Esc**+ |

> [!NOTE]
> 也可使用在 Visual Studio 其他位置所用的键盘快捷方式在“查看定义”窗口中编辑代码  。

## <a name="see-also"></a>另请参阅

- [导航代码](../ide/navigating-code.md)
- [转到定义和速览定义](../ide/go-to-and-peek-definition.md)
- [Visual Studio 中的工作效率功能](../ide/productivity-features.md)
