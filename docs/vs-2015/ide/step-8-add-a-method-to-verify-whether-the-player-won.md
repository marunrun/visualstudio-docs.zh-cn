---
title: 步骤 8：添加方法以验证玩家是否获胜 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: 6e317f6e-ba4c-4306-8924-300b0c2f65c6
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e2481693961dd03815381e9f71ee67cb73464bdf
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72646928"
---
# <a name="step-8-add-a-method-to-verify-whether-the-player-won"></a>步骤 8：添加方法以验证玩家是否获胜
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你已创建了一个有趣的游戏，但需要添加其他项来完成制作。 该游戏应当在玩家获胜时结束，因此您需要添加 `CheckForWinner()` 方法以验证玩家是否获胜。

### <a name="to-add-a-method-to-verify-whether-the-player-won"></a>添加方法以验证玩家是否获胜

1. 在你的代码底部，`CheckForWinner()` 事件处理程序下方添加一个 `timer1_Tick()` 方法，如以下代码所示。

     [!code-csharp[VbExpressTutorial4Step8#10](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step8/cs/form1.cs#10)]
     [!code-vb[VbExpressTutorial4Step8#10](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step8/vb/form1.vb#10)]

     该方法使用 `foreach` 循环（Visual C# 中）或 `For Each` 循环（Visual Basic 中）遍历 TableLayoutPanel 中的每个标签。 它使用相等运算符（在 Visual C# 中为 `==`，在 Visual Basic 中为 `=`）检查每个标签的图标颜色以验证它是否与背景匹配。 如果颜色匹配，图标将保持不可见，玩家还没有匹配所有剩余的图标。 在这种情况下，程序使用 `return` 语句跳过其余方法。 如果循环遍历所有标签而不执行 `return` 语句，则意味着窗体上的所有图标均已匹配。 该程序将显示一个恭喜玩家获胜的 MessageBox，然后调用窗体的 `Close()` 方法来结束游戏。

2. 接下来，让标签的 Click 事件处理程序调用新的 `CheckForWinner()` 方法。 请确保程序在显示玩家选择的第二个图标后立即检查是否有赢家。 查找设置第二个选中图标颜色的行，然后在其后直接调用 `CheckForWinner()` 方法，如以下代码所示。

     [!code-csharp[VbExpressTutorial4Step8#11](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step8/cs/form1.cs#11)]
     [!code-vb[VbExpressTutorial4Step8#11](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step8/vb/form1.vb#11)]

3. 保存并运行程序。 玩游戏并匹配所有图标。 当你获胜时，该程序将显示一个祝贺性的 MessageBox（如下图所示），然后关闭该框。

     ![与 MessageBox 匹配游戏](../ide/media/express-tut4step8.png "Express_Tut4Step8") 与 MessageBox 匹配游戏

### <a name="to-continue-or-review"></a>继续或查看

- 若要继续学习下一个教程，请参阅 [步骤9：尝试其他功能](../ide/step-9-try-other-features.md)。

- 若要返回上一个教程步骤，请参阅 [步骤7：保持对可见](../ide/step-7-keep-pairs-visible.md)。
