---
title: 步骤 2：运行程序 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: 9a8fe90e-c97b-4e98-b6c8-0c6b3962c49d
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 12bce61c7d860f56142c25dd15dea3ac8ad21f9c
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72671863"
---
# <a name="step-2-run-your-program"></a>步骤 2：运行程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

一旦创建新的解决方案，实际上就生成了所运行的程序。 该程序并未执行其他操作，它只是显示了一个在标题栏中显示“Form1”的空窗口。 但该程序确实在运行，您即将查明这一点。

 ![视频链接](../data-tools/media/playvideo.gif "PlayVideo")有关本主题的视频版本，请参阅[教程1：在 Visual Basic 中创建图片查看器-视频 1](http://go.microsoft.com/fwlink/?LinkId=205209)或[教程1：在视频1中C#创建图片查看器](http://go.microsoft.com/fwlink/?LinkId=205199)。 这些视频使用 Visual Studio 的早期版本，因此在一些菜单命令和其他用户界面元素上略有差异。 但是，概念和过程与当前版本的 Visual Studio 大同小异。

### <a name="to-run-your-program"></a>运行程序

1. 使用下列方法之一运行程序。

    - 选择 F5。

    - 在菜单栏上，依次选择“调试”、“开始调试”。

    - 在工具栏上，选择“开始调试”按钮，如下所示。

         "![开始调试" 工具栏按钮](../ide/media/express-icondebug.png "Express_IconDebug")"开始调试" 工具栏按钮

2. Visual Studio 将运行程序，并显示一个名为“Form1”的窗口。 下图显示了刚生成的程序。 该程序正在运行，您很快会向它添加内容。

     ![Windows 窗体应用程序正在运行](../ide/media/express-firstrun.png "Express_FirstRun")Windows 窗体应用程序正在运行

3. 返回 Visual Studio 集成开发环境 (IDE)，并查看新的工具栏。 当您运行程序时，工具栏上将显示其他按钮。 利用这些按钮，您可执行停止和启动程序之类的操作，并帮助您跟踪到可能具有的任何错误 (Bug)。 在本示例中，我们仅用它来启动和停止程序。

     ![调试工具栏](../ide/media/express-debugtoolbar.png "Express_DebugToolbar")调试工具栏

4. 使用下列方式之一停止程序。

    - 在工具栏上，选择“停止调试”按钮。

    - 在菜单栏上，依次选择“调试”、“停止调试”。

    - 选择“Form1”窗口上角的 X 按钮。

    > [!NOTE]
    > 在从 IDE 内部运行程序时，这一操作称为“调试”，因为通常将使用此操作来查找并修复程序中的 Bug（错误）。 虽然此程序很小，并且实际上不执行任何操作，但它仍是一个真正的程序。 您可以执行相同的过程来运行和调试其他程序。 要了解有关调试的详细信息，请参阅[调试程序基础知识](../debugger/debugger-basics.md)。

### <a name="to-continue-or-review"></a>继续或查看

- 要转到下一个教程步骤，请参阅[步骤 3：设置窗体属性](../ide/step-3-set-your-form-properties.md)。

- 要返回上一个教程步骤，请参阅[步骤 1：创建 Windows 窗体应用程序项目](../ide/step-1-create-a-windows-forms-application-project.md)。
