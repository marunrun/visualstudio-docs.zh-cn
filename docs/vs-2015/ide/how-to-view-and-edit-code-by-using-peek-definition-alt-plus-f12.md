---
title: 如何：使用查看定义查看和编辑代码 (Alt+F12) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: 45f3dd20-902a-4047-8cca-9f18216123f4
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 40772919031200466999df2dfbf651fae3ee01e7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72670573"
---
# <a name="how-to-view-and-edit-code-by-using-peek-definition-altf12"></a>如何：使用查看定义查看和编辑代码 (Alt+F12)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可使用“查看定义”命令来查看和编辑代码，而无需离开正在编写的代码。 “查看定义”和“转到定义”显示相同的信息，但“查看定义”在弹出窗口中显示，而“转到定义”在单独的代码窗口中显示代码   。 “转到定义”将导致上下文（即活动的代码窗口、当前行和光标位置）切换到定义代码窗口。 通过使用 " **速览定义**"，您可以查看和编辑定义，并在定义文件中移动，同时将您的位置保存在原始代码文件中。

 可对 C#、Visual Basic 和 C++ 代码使用“查看定义”。 在 Visual Basic 中，" **查看定义** " 显示一个链接，该链接指向没有定义元数据的符号的 **对象浏览器** (例如，) 中内置的 .NET Framework 类型。

> [!IMPORTANT]
> 你不能在任何 Visual Studio 2013 Express 版本中使用此命令。

## <a name="working-with-peek-definition"></a>使用“查看定义”

#### <a name="to-open-a-peek-definition-window"></a>打开“查看定义”窗口

1. 可通过打开要浏览的方法的快捷菜单来查找“查看定义”****。 （键盘：Alt+F12）

     本插图显示了名为 `Print()` 的方法的“查看定义”窗口：

     ![“查看”窗口](../ide/media/peekwindow.png "PeekWindow")

     定义窗口显示在原始文件的 `printer.Print(“Hello World!”)` 行的下方。 该窗口不会隐藏原始文件中的任何代码。 跟在 `printer.Print(“Hello World!”)` 调用后的行显示在定义窗口下。

2. 你可将光标移动到代码定义窗口中的不同位置。 你仍可在定义窗口上方或下方的原始代码窗口中移动。

3. 可从定义窗口中复制字符串，并将其粘贴在原始代码中。 也可将字符串从定义窗口拖放到原始代码中，而不从定义窗口中删除它。

4. 您可以通过选择 "Esc 键" 或 "定义窗口" 选项卡上的 " **关闭** " 按钮来关闭定义窗口。

#### <a name="to-open-a-peek-definition-window-from-within-a-peek-definition-window"></a>从“查看定义”窗口内部打开另一个“查看定义”窗口

- 如果“查看定义”窗口已打开，则可以对该窗口中的代码再次调用“查看定义” 。 此时将打开另一个定义窗口。 一组痕迹点将显示在定义窗口选项卡旁边，可用于在定义窗口之间导航。 每个点上的工具提示显示该点表示的定义文件的文件名和路径。

     ![“查看”窗口中的“查看”窗口](../ide/media/peekwithinpeek.png "PeekWithinPeek")

#### <a name="to-use-peek-definition-with-multiple-results"></a>使用“查看定义”时具有多个结果

- 如果对具有多个定义的代码（例如，分部类）使用“查看定义”，则代码定义视图的右侧将显示结果列表****。 你可选择列表中的任意结果来显示其定义。

     ![来自多个结果的“查看”窗口](../ide/media/peekmultiple.png "PeekMultiple")

#### <a name="to-edit-inside-the-peek-definition-window"></a>在“查看定义”窗口中编辑

- 开始在“查看定义”窗口中编辑时，所修改的文件将在代码编辑器中作为单独的选项卡自动打开，并显示已进行的更改****。 可在“查看定义”窗口中继续更改、撤消更改和保存更改，该选项卡将继续显示这些更改。 即使你关闭窗口时没有保存更改，也可以在窗口中上次离开的位置继续更改、撤消更改和保存更多更改。

     ![在“查看”窗口中编辑](../ide/media/peekedit.png "PeekEdit")

#### <a name="to-use-keyboard-shortcuts-for-peek-definition"></a>使用“查看定义”的键盘快捷键

- 可在“查看定义”窗口中使用下列键盘快捷方式：

    |功能|键盘快捷键|
    |-------------------|-----------------------|
    |打开定义窗口|Alt+F12|
    |关闭定义窗口|Esc|
    |将定义窗口提升为一个常规文档选项卡|Shift+Alt+Home|
    |在定义窗口间导航|Ctrl+Alt+- 和 Ctrl+Alt+=|
    |在多个结果间导航|F8 和 Shift+F8|
    |在代码编辑器窗口和定义窗口之间切换|Shift+Esc|

    > [!NOTE]
    > 也可使用在 Visual Studio 其他位置所用的键盘快捷方式在“查看定义”窗口中编辑代码。

## <a name="see-also"></a>另请参阅
 [工作效率提示](../ide/productivity-tips-for-visual-studio.md)
