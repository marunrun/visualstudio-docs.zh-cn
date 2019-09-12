---
title: 步骤 2：运行图片查看器应用
ms.date: 09/06/2019
ms.assetid: 9a8fe90e-c97b-4e98-b6c8-0c6b3962c49d
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
ms.openlocfilehash: a6c7e90f8113f5fa03da907db5dbb8f374a564e7
ms.sourcegitcommit: 4dfe098ac0df294aad63e6b384d6575980798ca3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2019
ms.locfileid: "70887917"
---
# <a name="step-2-run-your-picture-viewer-app"></a>步骤 2：运行图片查看器应用

创建 Windows 窗体应用项目时，实际上会生成一个运行的程序。 在本教程中，你的图片查看器应用程序不会执行任何其他操作，尽管可以执行。 它目前只是显示了一个在标题栏中显示“Form1”的空窗口  。

以下是运行应用的方法。 

1. 使用以下其中一种方法：

    - 选择 F5  。

    - 在菜单栏上，依次选择“调试”   > “开始调试”  。

    - 在工具栏上，选择“开始调试”按钮，如下所示  ：

      ![“开始调试”工具栏按钮](../ide/media/express_icondebug.png)<br>
      “开始调试”工具栏按钮 

1. Visual Studio 将运行应用，并显示一个名为“Form1”的窗口  。 以下屏幕截图显示了如何生成应用。 该应用正在运行，你很快会向它添加内容。

     ![Windows 窗体应用正在运行](../ide/media/express_firstrun.png)<br>
Windows 窗体应用正在运行 

1. 返回 Visual Studio 集成开发环境 (IDE)，然后查看新的工具栏。 运行应用程序时，工具栏上将显示其他按钮。 利用这些按钮，你可执行停止和启动应用之类的操作，并帮助你跟踪到可能出现的任何错误 (bug)。 在本例中，我们仅用它来启动和停止应用。

     ![调试工具栏](../ide/media/express_debugtoolbar.png)<br>
调试工具栏 

1. 使用以下其中一种方法停止应用：

    - 在工具栏上，选择“停止调试”按钮  。

    - 在菜单栏上，依次选择“调试”   > “停止调试”  。

    - 使用键盘，并按“Shift+F5”   。

    - 选择“Form1”  窗口上角的 X  按钮。

    > [!NOTE]
    > 在从 IDE 内部运行应用时，这一操作称为“调试”，因为通常将使用此操作来查找并修复应用程序中的 bug（错误）。 虽然此应用很小，并且实际上不执行任何操作，但它仍是一个真正的程序。 您可以执行相同的过程来运行和调试其他程序。 要了解有关调试的详细信息，请参阅[初探调试器](../debugger/debugger-feature-tour.md)。

## <a name="next-steps"></a>后续步骤

* 要转到下一个教程步骤，请参阅 **[步骤 3：设置窗体属性](../ide/step-3-set-your-form-properties.md)  。

* 若要返回上一个教程步骤，请参阅[步骤 1：创建 Windows 窗体应用项目](../ide/step-1-create-a-windows-forms-application-project.md)。

## <a name="see-also"></a>请参阅

* [教程 2：创建计时数学测验](tutorial-2-create-a-timed-math-quiz.md)
* [教程 3：创建匹配游戏](tutorial-3-create-a-matching-game.md)
