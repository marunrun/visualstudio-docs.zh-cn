---
title: 步骤 5：为 NumericUpDown 控件添加 Enter 事件处理程序
ms.date: 11/04/2016
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
dev_langs:
- CSharp
- VB
ms.assetid: 45a99a5d-c881-4298-b74d-adb481dec5ee
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 17fb9ba8e82739ddb0a420f52b6f7f945a6454b8
ms.sourcegitcommit: 2ae2436dc3484b9dfa10e0483afba1e5a02a52eb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/25/2020
ms.locfileid: "77579830"
---
# <a name="step-5-add-enter-event-handlers-for-the-numericupdown-controls"></a>步骤 5：为 NumericUpDown 控件添加 Enter 事件处理程序

在本教程的第 5 部分中，将添加 <xref:System.Windows.Forms.Control.Enter> 事件处理程序，以便在输入测验问题的答案时变得轻松一些。 当测验对象选择每个 <xref:System.Windows.Forms.NumericUpDown> 控件中的当前值并开始输入其他值时，此代码将立即选中并清除该当前值。

> [!NOTE]
> 本主题是基本编码概念教程系列中的一部分。 有关本教程的概述，请参阅[教程 2：创建计时数学测验](../ide/tutorial-2-create-a-timed-math-quiz.md)。

## <a name="to-verify-the-default-behavior"></a>验证默认行为

1. 运行您的程序，并开始测验。

     在加法题的 NumericUpDown  控件中，游标在“0”  （零）旁边闪烁。

2. 输入“3”  ，然后注意此控件将显示“30”  。

3. 输入“5”  ，然后请注意将显示“350”  ，但一秒后将更改为“100”  。

     在解决此问题之前，请先想想发生了什么事。 请考虑一下为什么当你输入“3”  时“0”  未消失，以及为什么“350”  会更改为“100”  但不是立即更改。

     此行为可能看似奇怪，但是考虑到代码的逻辑就可以说得通了。 选择“开始”按钮时，其“Enabled”属性设置为“False”，此按钮将显示为灰色且不可用。    您的程序会将当前选择（焦点）更改为具有最小 TabIndex 值的控件，即加法题的 NumericUpDown 控件。 当使用 Tab  键转到 NumericUpDown 控件时，光标将自动定位到此控件的起始位置，因此，你输入的数字将从左侧而不是右侧显示。 当指定的值大于“MaximumValue”属性的值（设置为 100）时，输入的数字将替换为该属性的值。 

## <a name="to-add-an-enter-event-handler-for-a-numericupdown-control"></a>为 NumericUpDown 控件添加 Enter 事件处理程序

1. 选择窗体上的第一个“NumericUpDown”  控件（名为“sum”），然后在“属性”  对话框中，选择工具栏上的“事件”  图标。

   ![属性工具栏中的“事件”按钮](media/control-properties-events.png)

   “属性”对话框中的“事件”选项卡显示窗体中所选项的所有可响应（处理）的事件。   由于您选择了 NumericUpDown 控件，因此所列出的事件都与此控件相关。

2. 选择“Enter”  事件，键入“`answer_Enter`”，再按 Enter  键。

   ![输入事件处理程序方法名称](media/enter-event.png)

   刚才已为 sum NumericUpDown 控件添加一个 Enter 事件处理程序，并将此处理程序命名为“answer_Enter”。 

3. 在“answer_Enter”  事件处理程序的方法中，添加以下代码：

     [!code-vb[VbExpressTutorial3Step5_6#11](../ide/codesnippet/VisualBasic/step-5-add-enter-event-handlers-for-the-numericupdown-controls_1.vb)]
     [!code-csharp[VbExpressTutorial3Step5_6#11](../ide/codesnippet/CSharp/step-5-add-enter-event-handlers-for-the-numericupdown-controls_1.cs)]

     [!INCLUDE [devlang-control-csharp-vb](./includes/devlang-control-csharp-vb.md)]

     此代码可能看起来复杂，但如果分步来看就可以理解。 首先，查看方法的顶部：在 C# 中为 `object sender`，在 Visual Basic 中为 `sender As System.Object`。 此参数引用已触发其事件的对象，即发送方。 在此示例中，发送方对象为 NumericUpDown 控件。 因此，在此方法的第一行中，您指定发送方不是任何一般对象，而是具体的 NumericUpDown 控件。 （每个 NumericUpDown 控件都是一个对象，但并不是每个对象都是 NumericUpDown 控件。）在此方法中，NumericUpDown 控件命名为“answerBox”，因为它将用于窗体上的所有 NumericUpDown 控件，而不仅是 sum NumericUpDown 控件。  由于您在此方法中声明了 answerBox 变量，因此其范围仅适用于此方法。 换言之，该变量只能在此方法内使用。

     下一行验证 answerBox 是否已成功地从一个对象转换（强制转换）为一个 NumericUpDown 控件。 如果转换不成功，此变量的值将为 `null` (C#) 或 `Nothing` (Visual Basic)。 第三行将获取 NumericUpDown 控件中所显示答案的长度，第四行将根据此长度选择控件中的当前值。 此时，当测试对象选择此控件时，Visual Studio 将触发此事件，从而选中当前答案。 一旦测试对象开始输入其他答案，之前的答案将被清除并替换为新答案。

4. 在“Windows 窗体设计器”  中，选择 difference“NumericUpDown”  控件。

5. 在“属性”对话框的“事件”页中，向下滚动到“Enter”事件，选择行末尾的下拉箭头，然后选择刚才添加的 `answer_Enter` 事件处理程序。   

6. 对 product 和 quotient NumericUpDown 控件重复上述步骤。

7. 保存您的程序，然后运行程序。

     当选择“NumericUpDown”  控件时，将自动选中现有值，然后在你开始输入其他值时自动清除现有值。

## <a name="to-continue-or-review"></a>继续或查看

- 要转到下一个教程步骤，请参阅[步骤 6：  添加减法题](../ide/step-6-add-a-subtraction-problem.md)。

- 要返回上一个教程步骤，请参阅[步骤 4：添加 CheckTheAnswer() 方法](../ide/step-4-add-the-checktheanswer-parens-method.md)。
