---
title: 步骤 3：添加一个倒计时计时器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: 62670a2b-efdc-45c6-9646-9b17eeb33dcb
caps.latest.revision: 25
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: d95708f940bfb12f67903f41d9f030a77877008d
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63442607"
---
# <a name="step-3-add-a-countdown-timer"></a>步骤 3：添加倒计时计时器
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在本教程的第 3 部分中，您将添加一个倒计时计时器，用于跟踪测验对象完成测验所剩秒数。  
  
> [!NOTE]
> 本主题是基本编码概念教程系列中的一部分。 有关本教程的概述，请参阅[教程 2：创建计时的数学测验](../ide/tutorial-2-create-a-timed-math-quiz.md)。  
  
### <a name="to-add-a-countdown-timer"></a>添加倒计时计时器  
  
1. 添加一个名为“timeLeft”的整型变量，就像在上一个过程中一样。 你的代码应类似以下内容。  
  
     [!code-csharp[VbExpressTutorial3Step3#5](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step3/cs/form1.cs#5)]
     [!code-vb[VbExpressTutorial3Step3#5](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step3/vb/form1.vb#5)]  
  
     现在您需要一个进行实际读秒的方法（例如计时器），此方法在您指定的时间后将引发一个事件。  
  
2. 在设计窗口中，将工具箱的“组件”类别中的 `Timer` 控件移到窗体中。  
  
     此控件显示在设计窗口底部的灰色区域内。  
  
3. 在窗体中，请选择刚才添加的“timer1”图标，并将其“Interval”属性设置为“1000”。  
  
     因为间隔值单位为毫秒，因此当值为 1000 时将使 Tick 事件每秒触发一次。  
  
4. 在窗体中，双击 Timer 控件，或将其选中，然后选择 Enter 键。  
  
     此时将出现代码编辑器，并显示您刚才添加的 Tick 事件处理程序的方法。  
  
5. 将下面的语句添加到新事件处理程序方法。  
  
     [!code-csharp[VbExpressTutorial3Step3#6](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step3/cs/form1.cs#6)]
     [!code-vb[VbExpressTutorial3Step3#6](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step3/vb/form1.vb#6)]  
  
     根据刚才添加的语句，计时器将每秒检查一次“timeLeft”整型变量是否大于 0，从而确定时间是否已用完。 如果大于 0，则表示仍有剩余时间。 首先，计时器从 timeLeft 中减去 1，然后更新 `timeLabel` 控件的“Text”属性，以便向测验者显示剩余的秒数。  
  
     如果没有剩余时间，则计时器停止并更改 `timeLabel` 控件的文本，使之显示“Time's up!”（时间到!）。 此时将通过一个消息框宣布测验结束，并公布答案，在此示例中，是将 addend1 和 addend2 相加。 将 `startButton` 控件的“Enabled”属性设置为 `true`，以便测验者开始其他测试。  
  
     您刚刚添加了 `if else` 语句，可通过这种方式告诉程序做出判断。 `if else` 语句如下所示。  
  
    > [!NOTE]
    > 下面的示例仅用于说明，请勿将其添加到您的项目。  
  
    ```vb  
    If (something that your program will check) Then  
        ' One or more statements that will run  
        ' if what the program checked is true.   
    Else  
        ' One or more statements that will run  
        ' if what the program checked is false.  
    End If  
    ```  
  
    ```csharp  
    if (something that your program will check)  
    {  
        // One or more statements that will run  
        // if what the program checked is true.   
    }  
    else  
    {  
        // One or more statements that will run  
        // if what the program checked is false.  
    }  
    ```  
  
     请仔细查看您刚才在 `else` 块中添加的、用于显示加法题答案的语句。  
  
     [!code-csharp[VbExpressTutorial3Step3#24](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step3/cs/form1.cs#24)]
     [!code-vb[VbExpressTutorial3Step3#24](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step3/vb/form1.vb#24)]  
  
     语句 `addend1 + addend2` 会将两个变量中的值相加。 第一部分 (`sum.Value`) 使用 sum `NumericUpDown` 控件的“Value”属性来显示正确答案。 您稍后将使用相同的属性来检查测验的答案。  
  
     测验者可以使用 `NumericUpDown` 控件更轻松地输入数字，因此将此控件用于数学问题的回答。 所有可能的答案均为 0 到 100 之间的整数。 通过保留“Minimum”、“Maximum”和“DecimalPlaces”属性的默认值，可以确保测验者不能输入小数、负数或过大的数字。 （如果要允许测验者输入 3.141 但不允许输入 3.1415，则可以将“DecimalPlaces”属性设置为 3。）  
  
6. 将三行代码添加到 `StartTheQuiz()` 方法的结尾，以使代码类似于下面这样。  
  
     [!code-csharp[VbExpressTutorial3Step3#7](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step3/cs/form1.cs#7)]
     [!code-vb[VbExpressTutorial3Step3#7](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step3/vb/form1.vb#7)]  
  
     现在，当测验开始时，“timeLeft”变量将设置为 30，而 `timeLabel` 控件的“Text”属性将设置为 30 秒。 然后，`Timer` 控件的 `Start()` 方法开始倒计时。 （测验现在还不会检查答案，接下来将介绍此内容。）  
  
7. 保存并运行程序，然后选择窗体上的“开始”按钮。  
  
     计时器将开始倒计时。 当时间用完时，测验将结束，并显示答案。 下图显示了正在进行的测验。  
  
     ![正在进行数学测验](../ide/media/express-addcountdown.png "Express_AddCountdown")  
数学测验正在进行中  
  
### <a name="to-continue-or-review"></a>继续或查看  
  
- 要转到下一个教程步骤，请参阅[步骤 4：添加 checktheanswer （） 方法](../ide/step-4-add-the-checktheanswer-parens-method.md)。  
  
- 要返回上一个教程步骤，请参阅[步骤 2：创建随机加法问题](../ide/step-2-create-a-random-addition-problem.md)。
