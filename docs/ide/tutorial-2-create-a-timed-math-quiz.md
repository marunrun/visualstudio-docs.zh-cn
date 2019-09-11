---
title: 教程 2：创建计时数学测验
ms.date: 11/04/2016
ms.assetid: d7165d08-ace3-457d-b57d-fb8f80760a6f
ms.topic: tutorial
ms.technology: vs-ide-general
ms.devlang:
- csharp
- vb
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c0c7f3695be87f6cb4081b3aa02fc7a129869a4c
ms.sourcegitcommit: 9c07ae6fb18204ea080c8248994a683fa12e5c82
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2019
ms.locfileid: "70293697"
---
# <a name="tutorial-2-create-a-timed-math-quiz"></a>教程 2：创建计时数学测验

在本教程中，您将构建一个测验，在该测验中，测验对象必须在指定时间内回答四道随机算术题。 您将学习如何：

- 使用 <xref:System.Random> 类生成随机数。

- 使用 <xref:System.Windows.Forms.Timer> 控件触发事件，使之在特定时间发生。

- 使用 `if else` 语句控制程序流。

- 使用代码执行基本算术运算。

完成时，你的测验看上去与下图类似，但数字有所不同。

![包含四个问题的数学测验](../ide/media/express_finishedquiz.png)

## <a name="tutorial-links"></a>教程链接

若要下载测验的完整版本，请参阅[数学测验教程的完整示例](https://code.msdn.microsoft.com/Complete-Math-Quiz-8581813c)。

> [!NOTE]
> 本教程中同时涉及 Visual C# 和 Visual Basic，因此请关注特定于您所用编程语言的信息。

## <a name="related-topics"></a>相关主题

|Title|说明|
|-----------|-----------------|
|[步骤 1：创建项目并向窗体添加标签](../ide/step-1-create-a-project-and-add-labels-to-your-form.md)|首先创建项目，更改属性并添加 `Label` 控件。|
|[步骤 2：创建随机加法问题](../ide/step-2-create-a-random-addition-problem.md)|创建一道加法题，然后使用 `Random` 类生成随机数。|
|[步骤 3：添加倒计时计时器](../ide/step-3-add-a-countdown-timer.md)|添加一个倒计时计时器，以便对测验进行计时。|
|[步骤 4：添加 CheckTheAnswer() 方法](../ide/step-4-add-the-checktheanswer-parens-method.md)|添加一个方法，用于检查测验对象输入的问题答案是否正确。|
|[步骤 5：为 NumericUpDown 控件添加 Enter 事件处理程序](../ide/step-5-add-enter-event-handlers-for-the-numericupdown-controls.md)|添加事件处理程序，使您的测验更易于进行。|
|[步骤 6：添加减法问题](../ide/step-6-add-a-subtraction-problem.md)|添加一道可生成随机数的减法题，使用计时器并检查答案是否正确。|
|[步骤 7：添加乘法和除法问题](../ide/step-7-add-multiplication-and-division-problems.md)|添加可生成随机数的乘法和除法题，使用计时器并检查答案是否正确。|
|[步骤 8：自定义测验](../ide/step-8-customize-the-quiz.md)|尝试其他功能，例如更改颜色和添加提示。|
