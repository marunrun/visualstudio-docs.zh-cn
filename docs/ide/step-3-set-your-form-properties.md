---
title: 步骤 3：设置窗体属性
ms.date: 08/30/2019
ms.assetid: 634ef037-1525-48c8-ac7f-abf04be69376
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.devlang:
- csharp
- vb
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: da1ca71cb420bcc2bbc6ba00eb1eca5deaa2b2c9
ms.sourcegitcommit: 4dfe098ac0df294aad63e6b384d6575980798ca3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2019
ms.locfileid: "70887901"
---
# <a name="step-3-set-your-form-properties"></a>步骤 3：设置窗体属性

接下来，使用“属性”窗口更改窗体的外观  。

## <a name="how-to-set-your-form-properties"></a>如何设置窗体属性

1. 确保你查看的是 Windows 窗体设计器  。 在 Visual Studio 集成开发环境 (IDE) 中，选择“Form1.cs [设计]”选项卡（或 Visual Basic 中的“Form1.vb [设计]”）   。

1. 选择“Form1”窗体中的任意位置以将其选定  。 查看“属性”窗口，该窗口此时应显示窗体的属性  。 窗体具有各种属性。 例如，可以设置前景色和背景色、窗体顶部显示的标题文本、窗体的大小和其他属性。

   > [!NOTE]
   > 如果“属性”窗口未出现，请通过选择工具栏上的正方形“停止调试”按钮来停止应用或直接关闭窗口   。 如果应用已停止，且仍未显示“属性”窗口，请在菜单栏上选择“视图” > “属性”窗口    。

1. 选中窗体后，在“属性”窗口中找到“Text”属性   。 根据列表排序的方式，您可能需要向下滚动。 选择“Text”  ，键入“图片查看器”  ，然后按 Enter  。  窗体的标题栏中将显示文本“图片查看器”，并且“属性”窗口的外观应与以下屏幕截图类似   。

    ![属性窗口](../ide/media/express_edittextproperty.png)<br>
   属性窗口 

   > [!NOTE]
   > 可以通过“按分类顺序”  视图或“字母顺序”  视图对属性进行排序。 可通过使用“属性”窗口上的按钮在这两类视图之间进行切换  。 在本教程中，通过“字母顺序”  视图查找属性会更加轻松。

1. 返回“Windows 窗体设计器”  。 选择窗体右下角的拖动手柄，此拖动手柄是位于窗体右下角的白色小正方形，如下所示。

    ![拖动句柄](../ide/media/express_bottomrt_drag.png)<br>
   拖动句柄 

    拖动手柄以调整窗体的大小，使其更宽且更高一些。

1. 查看“属性”窗口，你会发现“Size”属性已更改   。 每次重设窗体的大小时，“Size”属性都会更改  。 尝试拖动窗体的手柄以将其大小调整为大约 550 x 350  （无需精确），这个大小应适合于此项目。 或者，可以直接在“Size”  属性中输入值，然后按 Enter  。

1. 再次运行应用。 记住，你可以使用以下任何一种方法来运行应用。

   - 选择 F5  。

   - 在菜单栏上，依次选择“调试”   > “开始调试”  。

   - 在工具栏上，选择“开始调试”按钮，如下所示  。

      ![“开始调试”工具栏按钮](../ide/media/express_icondebug.png)<br>
     “开始调试”工具栏按钮 

     与之前的操作一样，IDE 会生成并运行应用，并且将显示一个窗口。

1. 在转到下一个步骤之前，请停止应用，因为 IDE 不允许你在应用处于运行状态时更改应用。 记住，你可以使用以下任何一种方法来停止应用。

   - 在工具栏上，选择“停止调试”按钮  。

   - 在菜单栏上，依次选择“调试”   > “停止调试”  。

   - 使用键盘，并按“Shift+F5”   。

   - 选择“图片查看器”窗口上角的“X”按钮   。

## <a name="next-steps"></a>后续步骤

* 要转到下一个教程步骤，请参阅[步骤 4：使用 TableLayoutPanel 控件设置窗体布局](../ide/step-4-lay-out-your-form-with-a-tablelayoutpanel-control.md)  。

* 要返回上一个教程步骤，请参阅[步骤 2：运行图片查看器应用(../ide/step-2-run-your-program.md)。

## <a name="see-also"></a>请参阅

* [教程 2：创建计时数学测验](tutorial-2-create-a-timed-math-quiz.md)
* [教程 3：创建匹配游戏](tutorial-3-create-a-matching-game.md)
