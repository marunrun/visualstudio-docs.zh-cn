---
title: 如何：使用查找程序工具 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Window Finder Tool
ms.assetid: 5841926b-08c3-4e43-88bd-4223d04f9aef
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f96fe87137c6b14e32fb2648e93c54a1c5b094a0
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72732165"
---
# <a name="how-to-use-the-finder-tool"></a>如何：使用查找程序工具
您可以使用 "**查找窗口**" 对话框中的 "查找程序" 工具显示窗口属性或消息。 查找器工具还可以查找已禁用的子窗口，并识别在禁用的子窗口重叠时要突出显示的窗口。

 !["&#43; &#43;监视查找窗口" 对话框](../debugger/media/icon_spy--_find.png "Icon_Spy + + _Find")"查找窗口" 对话框中的查找器工具

 上图显示了下面的步骤3后面的 "查找窗口" 对话框。

### <a name="to-display-window-properties-or-messages"></a>显示窗口属性或消息

1. 排列窗口，使 Spy + + 和目标窗口可见。

2. 从**Spy**菜单中，选择 "**查找窗口**"。

    "[查找窗口" 对话框](../debugger/find-window-dialog-box.md)将打开。

3. 将 "**查找程序工具**" 拖到目标窗口上。

    拖动工具时，"**查找窗口**" 对话框将显示所选窗口的详细信息。

   - 或 -

     如果您有要检查的窗口的句柄（例如，从调试器复制），请在 "**句柄**" 文本框中键入。

   > [!TIP]
   > 若要减少屏幕干扰，请选择 "**隐藏 Spy** " 选项。 此选项将隐藏 Spy + + 主窗口，使 "**查找窗口**" 对话框仅在其他应用程序上可见。 当你单击 **"确定" 或 "** **取消**" 时，或者在清除 "**隐藏 Spy + +** " 选项时，将还原 spy + + 主窗口。

4. 在 "**显示**" 下，选择 "**属性**" 或 "**消息**"。

5. 按“确定”。

    如果选择了 "**属性**"，则 "[窗口属性" 对话框](../debugger/window-properties-dialog-box.md)将打开。 如果选择了 "**消息**"，则将打开 "[消息视图](../debugger/messages-view.md)" 窗口。

## <a name="see-also"></a>请参阅
- [Spy++ 视图](../debugger/spy-increment-views.md)
- [使用 Spy++](../debugger/using-spy-increment.md)
- [Spy++ 参考](../debugger/spy-increment-reference.md)