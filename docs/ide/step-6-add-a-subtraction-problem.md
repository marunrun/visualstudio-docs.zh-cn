---
title: 步骤 6：添加减法问题
ms.date: 11/04/2016
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
dev_langs:
- CSharp
- VB
ms.assetid: 59204ef9-24bd-4f81-b85f-e3168e518a3e
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c3c6eed20fc1f2b76c02865c2a5f6b21cde1ae51
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75589989"
---
# <a name="step-6-add-a-subtraction-problem"></a>步骤 6：添加减法问题
在本教程的第 6 部分中，你将添加一道减法题并了解如何执行以下任务：

- 存储做减法的值。

- 生成用于提问的随机数字，并确保答案介于 0 和 100 之间。

- 更新用于检查答案的方法，使之同时检查新添加的减法题。

- 更新计时器的 <xref:System.Windows.Forms.Timer.Tick> 事件处理程序，以便此事件处理程序在时间用完之前会填写出正确答案。

> [!NOTE]
> 本主题是基本编码概念教程系列中的一部分。
> - 有关本教程的概述，请参阅[教程 2：创建计时数学测验](../ide/tutorial-2-create-a-timed-math-quiz.md)。
> - 若要下载完整版代码，请参阅[数学测验教程的完整示例](https://code.msdn.microsoft.com/Complete-Math-Quiz-8581813c)。

## <a name="to-add-a-subtraction-problem"></a>添加减法问题

1. 将此减法题的两个整型变量添加到窗体中，并放置在加法题和计时器的整型变量之间。 代码应如下所示。

     [!code-vb[VbExpressTutorial3Step5_6#12](../ide/codesnippet/VisualBasic/step-6-add-a-subtraction-problem_1.vb)]
     [!code-csharp[VbExpressTutorial3Step5_6#12](../ide/codesnippet/CSharp/step-6-add-a-subtraction-problem_1.cs)]

     [!INCLUDE [devlang-control-csharp-vb](./includes/devlang-control-csharp-vb.md)]

     新的整型变量的名称（“minuend”和“subtrahend”）不是编程术语。   它们是传统的算术名称，分别是指要减去的数字（subtrahend，减数）和从中减去减数的数字（minuend，被减数）。 差值是被减数减去减数的结果。 你可以使用其他名称，因为程序不要求变量、控件、组件或方法使用特定的名称。 你必须遵循诸如名称不得以数字开头等规则，但通常可以使用 x1、、x2、x3 和 x4 等名称。 但是，通用名称会使代码难以理解，而且几乎无法查明问题。 为了使变量名称保持唯一性和有用性，在本教程的后面部分中，你将使用传统的乘法名称（multiplicand × multiplier = product，被乘数 × 乘数 = 积）和除法名称（dividend ÷ divisor = quotient，被除数 ÷ 除数 = 商）。

     接下来，您将修改 `StartTheQuiz()` 方法，以便为减法题提供随机值。

2. 将下面的代码添加到“Fill in the subtraction problem”注释之后。

     [!code-vb[VbExpressTutorial3Step5_6#13](../ide/codesnippet/VisualBasic/step-6-add-a-subtraction-problem_2.vb)]
     [!code-csharp[VbExpressTutorial3Step5_6#13](../ide/codesnippet/CSharp/step-6-add-a-subtraction-problem_2.cs)]

     为了避免减法题答案为负，此代码在 <xref:System.Random.Next> 类 <xref:System.Random> 方法的使用方式上与加法题略有不同。 当您为 `Next()` 方法赋予两个值时，它会选取一个大于等于第一个值但小于第二个值的随机数。 下面的代码将从 1 到 100 之间选择一个随机数，并将其存储在 minuend 变量中。

     [!code-vb[VbExpressTutorial3Step5_6#21](../ide/codesnippet/VisualBasic/step-6-add-a-subtraction-problem_3.vb)]
     [!code-csharp[VbExpressTutorial3Step5_6#21](../ide/codesnippet/CSharp/step-6-add-a-subtraction-problem_3.cs)]

     可以用多种方法调用 Random 类的 `Next()` 方法，在本教程的前面部分中，已将此类命名为“randomizer”。 可使用多种方式调用的方法称为重载，您可以使用 IntelliSense 来探索这些方法。 请再次查看 IntelliSense 窗口中关于 `Next()` 方法的工具提示。

     ![IntelliSense 窗口工具提示](../ide/media/express_overloads.png)<br/>
IntelliSense 窗口工具提示 

     此工具提示显示“(+ 2 重载)”，这意味着可以用另外两种方法来调用 `Next()` 方法。  重载包含不同数量或类型的自变量，因此，它们的工作方式彼此略有不同。 例如，某个方法可能只采用一个整型参数，而其重载之一则可能采用一个整数和一个字符串。 您应选择正确的重载，使之执行您所需操作。 将代码添加到 `StartTheQuiz()` 方法时，只要输入 `randomizer.Next(`，IntelliSense 窗口中将显示详细信息。 若要循环显示重载，请选择向上键  和向下键  ，如下图所示：

     ![IntelliSense 中 Next&#40;&#41; 方法的重载](../ide/media/express_nextoverload.png)<br/>
IntelliSense 中 Next() 方法  的重载 

     在此示例中，您想要选择最后一个重载，因为您可以指定最小值和最大值。

3. 修改 `CheckTheAnswer()` 方法来检查减法答案是否正确。

     [!code-vb[VbExpressTutorial3Step5_6#14](../ide/codesnippet/VisualBasic/step-6-add-a-subtraction-problem_4.vb)]
     [!code-csharp[VbExpressTutorial3Step5_6#14](../ide/codesnippet/CSharp/step-6-add-a-subtraction-problem_4.cs)]

     在 C# 中，`&&` 是 `logical and` 运算符。 在 Visual Basic 中，等效的运算符是 `AndAlso`。 这些运算符表示“addend1 和 addend2 的和是否等于 sum NumericUpDown 的值，并且 minuend 减去 subtrahend 是否等于 difference NumericUpDown 的值”。 仅当加法题和减法题的答案都正确时，`CheckTheAnswer()` 方法才会返回 `true`。

4. 将计时器 Tick 事件处理程序的最后部分替换为下面的代码，使其在时间用完时填充正确答案。

     [!code-vb[VbExpressTutorial3Step5_6#22](../ide/codesnippet/VisualBasic/step-6-add-a-subtraction-problem_5.vb)]
     [!code-csharp[VbExpressTutorial3Step5_6#22](../ide/codesnippet/CSharp/step-6-add-a-subtraction-problem_5.cs)]

5. 保存并运行代码。

     如下图所示，你的程序包括一道减法题：

     ![带减法题的数学测验](../ide/media/express_addsubtract.png)<br/>
有减法问题  的数学测验

## <a name="to-continue-or-review"></a>继续或查看

- 要转到下一个教程步骤，请参阅[步骤 7：添加乘法和除法题](../ide/step-7-add-multiplication-and-division-problems.md)  。

- 要返回上一个教程步骤，请参阅[步骤 5：为 NumericUpDown 控件添加 Enter 事件处理程序](../ide/step-5-add-enter-event-handlers-for-the-numericupdown-controls.md)。
