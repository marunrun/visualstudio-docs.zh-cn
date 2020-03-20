---
title: 步骤 3：向每个标签分配一个随机图标
ms.date: 11/04/2016
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
dev_langs:
- CSharp
- VB
ms.assetid: 0ba5ed7a-9aaa-41f4-95d2-e3c2d567bc79
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 366f6d7a07d2f30b5b8110fb7dae7a2311fcce23
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "77579393"
---
# <a name="step-3-assign-a-random-icon-to-each-label"></a>步骤 3：向每个标签分配一个随机图标

如果图标显示在每个游戏的相同单元格中，就不是很有挑战性。 为避免这种情况，请使用 `AssignIconsToSquares()` 方法将图标随机分配给 Label 控件。

## <a name="to-assign-a-random-icon-to-each-label"></a>向每个标签分配一个随机图标

1. 在添加以下代码之前，请考虑该方法的工作原理。 有一个新的关键字：`foreach`（C# 中）或 `For Each`（Visual Basic 中）。 （其中有一行被故意注释掉，本过程的结尾对此进行了解释）。

     [!code-csharp[VbExpressTutorial4Step2_3_4#2](../ide/codesnippet/CSharp/step-3-assign-a-random-icon-to-each-label_1.cs)]
     [!code-vb[VbExpressTutorial4Step2_3_4#2](../ide/codesnippet/VisualBasic/step-3-assign-a-random-icon-to-each-label_1.vb)]

      > [!IMPORTANT]
      > 使用此页右上角的编程语言控件查看 C# 代码片段或 Visual Basic 代码片段。<br><br>![Docs.Microsoft.com 的编程语言控件](../ide/media/docs-programming-language-control.png)

2. 按上一步骤所示，添加 `AssignIconsToSquares()` 方法。 可以就将它置于在[步骤 2：添加 Random 对象和图标列表](../ide/step-2-add-a-random-object-and-a-list-of-icons.md)中添加的列表拉取随机图标。

     前面提到，`AssignIconsToSquares()` 方法中有一个新增功能：`foreach` 循环（在 C# 中）和 `For Each`（在 Visual Basic 中）。 无论何时想要多次执行相同操作，你都可以使用 `For Each` 循环。 在本例中，要对 <xref:System.Windows.Forms.TableLayoutPanel> 中的每个标签执行相同的语句，下面的代码对此进行了解释。 第一行创建一个名为 `control` 的变量，该变量在每个控件执行循环中的语句时存储一次该控件。

     [!code-csharp[VbExpressTutorial4Step2_3_4#14](../ide/codesnippet/CSharp/step-3-assign-a-random-icon-to-each-label_2.cs)]
     [!code-vb[VbExpressTutorial4Step2_3_4#14](../ide/codesnippet/VisualBasic/step-3-assign-a-random-icon-to-each-label_2.vb)]

    > [!NOTE]
    > 其中使用了名称“iconLabel”和“control”，是因为它们具有描述性。 你可以将这些名称替换为任何名称，代码的运行将完全相同（只要你更改循环内每个语句中的名称）。

     `AssignIconsToSquares()` 方法将迭代 TableLayoutPanel 中的每个标签控件，并对每个控件执行相同的语句。 这些语句从你在[步骤 2：添加 Random 对象和图标列表](../ide/step-2-add-a-random-object-and-a-list-of-icons.md)中添加的列表拉取随机图标。 （这就是该列表中每个图标都有两个的原因，因此将向随机 Label 控件分配一对图标。）

     更加仔细地观察 `foreach` 或 `For Each` 循环中运行的代码。 此代码将在此处重现。

     [!code-csharp[VbExpressTutorial4Step2_3_4#16](../ide/codesnippet/CSharp/step-3-assign-a-random-icon-to-each-label_3.cs)]
     [!code-vb[VbExpressTutorial4Step2_3_4#16](../ide/codesnippet/VisualBasic/step-3-assign-a-random-icon-to-each-label_3.vb)]

     第一行将 control  变量转换为名为“iconLabel”  的标签。 第一行之后的行是检查以确保转换起作用的 `if` 语句。 如果转换起作用，则 `if` 语句中的语句将运行。 （你可以回想前面的教程，`if` 语句用于计算你指定的任何条件）。`if` 语句中的第一行将创建一个名为“randomNumber”  的变量，该变量包含一个与图标列表中的项对应的随机数。 为此，它使用你之前创建的 <xref:System.Random.Next> 对象的 <xref:System.Random> 方法。 `Next` 方法将返回此随机数。 此行也使用“图标”  列表的 <xref:System.Collections.Generic.List%601.Count> 属性来确定随机数的选择范围。 下一行会将图标列表项之一分配给标签的 <xref:System.Windows.Forms.Label.Text> 属性。 本主题后面的部分将介绍已注释掉的行。 最后，`if` 语句中最后一行将从列表中删除已添加到窗体中的图标。

     请记住，如果你不确定部分代码的行为，可将鼠标指针定位在代码元素的上方，并查看生成的工具提示。 你还可以在使用 Visual Studio 调试器运行程序时，逐步调试每行代码。 有关详细信息，请参阅[如何：在 Visual Studio 中使用调试器逐步调试？](https://msdn.microsoft.com/vstudio/ee672313.aspx)或[使用调试器浏览代码](../debugger/navigating-through-code-with-the-debugger.md)。

3. 若要用图标填充游戏板，你需要在程序启动时调用 `AssignIconsToSquares()` 方法。 如果使用 C#，则在 Form1 构造函数中 `InitializeComponent()` 方法调用下方直接添加一条语句，这样窗体便可以调用新方法以在显示之前对自身进行设置   。 创建新对象（例如类或结构）时，将调用构造函数。 有关详细信息，请参阅 Visual Basic 中的[构造函数（C# 编程指南）](/dotnet/csharp/programming-guide/classes-and-structs/constructors)或[使用构造函数和析构函数](/previous-versions/visualstudio/visual-studio-2008/2z08e49e\(v\=vs.90\))。

     [!code-csharp[VbExpressTutorial4Step2_3_4#13](../ide/codesnippet/CSharp/step-3-assign-a-random-icon-to-each-label_4.cs)]

     对于 Visual Basic，将 `AssignIconsToSquares()` 方法调用添加到 `Form1_Load` 方法，以使代码如下所示。

    ```vb
    Private Sub Form1_Load(sender As Object, e As EventArgs) Handles MyBase.Load
        AssignIconsToSquares()
    End Sub
    ```

4. 保存并运行程序。 它应该显示一个窗体，其中每个标签都分配了随机图标。

5. 关闭程序，然后重新运行。 请注意，每个标签都分配了不同的图标，如下图所示。

     ![具有随机图标的匹配游戏](../ide/media/express_tut4step3.png)<br/>
*具有随机图标的匹配游戏*

     你没有隐藏这些图标，所以现在可以看到。 若要向玩家隐藏图标，可以将每个标签的“ForeColor”  属性设置为与“BackColor”  属性相同的颜色。

    > [!TIP]
    > 隐藏标签等控件的另一种方法是，将其“Visible”  属性设置为“false”  。

6. 若要隐藏图标，请停止程序并删除 `For Each` 循环内代码注释行上的注释标记。

     [!code-csharp[VbExpressTutorial4Step2_3_4#15](../ide/codesnippet/CSharp/step-3-assign-a-random-icon-to-each-label_5.cs)]
     [!code-vb[VbExpressTutorial4Step2_3_4#15](../ide/codesnippet/VisualBasic/step-3-assign-a-random-icon-to-each-label_5.vb)]

7. 在菜单栏上，选择“全部保存”  按钮保存程序，然后运行该程序。 图标看起来消失了 - 只显示蓝色背景。 但是，图标是随机分配的，仍然存在。 因为图标与背景颜色相同，所以玩家看不到它们。 毕竟，如果玩家能立即看到所有图标，游戏就没有挑战性了！

## <a name="to-continue-or-review"></a>继续或查看

- 要转到下一个教程步骤，请参阅[步骤 4：  向每个标签添加一个 Click 事件处理程序](../ide/step-4-add-a-click-event-handler-to-each-label.md)。

- 要返回上一个教程步骤，请参阅[步骤 2：添加 Random 对象和图标列表](../ide/step-2-add-a-random-object-and-a-list-of-icons.md)中添加的列表拉取随机图标。
