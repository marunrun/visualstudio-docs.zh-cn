---
title: 步骤 3：向每个标签分配一个随机图标 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: 0ba5ed7a-9aaa-41f4-95d2-e3c2d567bc79
caps.latest.revision: 33
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: d65d1a758523aaf7652f2d47bec50aa9fdb91884
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65694011"
---
# <a name="step-3-assign-a-random-icon-to-each-label"></a>步骤 3：向每个标签分配一个随机图标
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果图标显示在每个游戏的相同单元格中，就不是很有挑战性。 为避免这种情况，请使用 `AssignIconsToSquares()` 方法将图标随机分配给标签控件。  
  
### <a name="to-assign-a-random-icon-to-each-label"></a>向每个标签分配一个随机图标  
  
1. 在添加以下代码之前，请考虑该方法的工作原理。 有一个新的关键字：`foreach`（Visual C# 中）或 `For Each`（Visual Basic 中）。 （其中有一行被故意注释掉，本过程的结尾对此进行了解释）。  
  
     [!code-csharp[VbExpressTutorial4Step2_3_4#2](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/cs/form1.cs#2)]
     [!code-vb[VbExpressTutorial4Step2_3_4#2](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/vb/form1.vb#2)]  
  
2. 按上一步骤所示，添加 `AssignIconsToSquares()` 方法。 可以就将它置于在[步骤 2：添加随机对象和图标列表](../ide/step-2-add-a-random-object-and-a-list-of-icons.md)。  
  
     前面提到，`AssignIconsToSquares()` 方法中有一个新增功能：`foreach` 循环（在 Visual C# 中）和 `For Each`（在 Visual Basic 中）。 无论何时想要多次执行相同操作，你都可以使用 `For Each` 循环。 在本例中，你要对 TableLayoutPanel 中的每个标签执行相同的语句，下面的代码对此进行了解释。 第一行创建一个名为 `control` 的变量，该变量在每个控件执行循环中的语句时存储一次该控件。  
  
     [!code-csharp[VbExpressTutorial4Step2_3_4#14](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/cs/form1.cs#14)]
     [!code-vb[VbExpressTutorial4Step2_3_4#14](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/vb/form1.vb#14)]  
  
    > [!NOTE]
    > 其中使用了名称“iconLabel”和“control”，是因为它们具有描述性。 你可以将这些名称替换为任何名称，代码的运行将完全相同（只要你更改循环内每个语句中的名称）。  
  
     `AssignIconsToSquares()` 方法将迭代 TableLayoutPanel 中的每个标签控件，并对每个控件执行相同的语句。 这些语句从你在[步骤 2：添加随机对象和图标列表](../ide/step-2-add-a-random-object-and-a-list-of-icons.md)。 （这就是该列表中每个图标都有两个的原因，因此将向随机标签控件分配一对图标。）  
  
     更加仔细地观察 `foreach` 或 `For Each` 循环中运行的代码。 此代码将在此处重现。  
  
     [!code-csharp[VbExpressTutorial4Step2_3_4#16](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/cs/form1.cs#16)]
     [!code-vb[VbExpressTutorial4Step2_3_4#16](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/vb/form1.vb#16)]  
  
     第一行将 `control` 变量转换为名为 `iconLabel` 的标签。 第一行之后的行是检查以确保转换起作用的 `if` 语句。 如果转换起作用，则 `if` 语句中的语句将运行。 （你可以回想前面的教程，`if` 语句用于计算你指定的任何条件）。`if` 语句中的第一行将创建一个名为 `randomNumber` 的变量，该变量包含一个与图标列表中的项对应的随机数。 为此，它使用你之前创建的 `Next` 对象的 `Random` 方法。 `Next` 方法将返回此随机数。 此行也使用 `Count` 列表的 `icons` 属性来确定随机数的选择范围。 下一行会将图标列表项之一分配给标签的 `Text` 属性。 本主题后面的部分将介绍已注释掉的行。 最后，`if` 语句中最后一行将从列表中删除已添加到窗体中的图标。  
  
     请记住，如果你不确定部分代码的行为，可将鼠标指针定位在代码元素的上方，并查看生成的工具提示。 你还可以在使用 Visual Studio 调试器运行程序时，逐步调试每行代码。 请参阅[如何实现：使用 Visual Studio 中调试程序步骤？](https://msdn.microsoft.com/vstudio/ee672313.aspx)或[使用调试器浏览代码](../debugger/navigating-through-code-with-the-debugger.md)有关详细信息。  
  
3. 若要用图标填充游戏板，你需要在程序启动时调用 `AssignIconsToSquares()` 方法。 如果使用 Visual C#，则在 `Form1` 构造函数中 `InitializeComponent()` 方法调用下方直接添加一条语句，这样窗体便可以调用新方法以在显示之前对自身进行设置。 创建新对象（例如类或结构）时，将调用构造函数。 有关详细信息，请参阅 Visual Basic 中的[构造函数（C# 编程指南）](https://msdn.microsoft.com/library/ace5hbzh.aspx)或[使用构造函数和析构函数](https://msdn.microsoft.com/library/2z08e49e%28v=vs.90%29.aspx)。  
  
     [!code-csharp[VbExpressTutorial4Step2_3_4#13](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/cs/form1.cs#13)]  
  
     对于 Visual Basic，将 `AssignIconsToSquares()` 方法调用添加到 `Form1_Load` 方法，以使代码如下所示。  
  
    ```vb  
    Private Sub Form1_Load(sender As Object, e As EventArgs) Handles MyBase.Load  
        AssignIconsToSquares()  
    End Sub  
    ```  
  
4. 保存并运行程序。 它应该显示一个窗体，其中每个标签都分配了随机图标。  
  
5. 关闭程序，然后重新运行。 请注意，每个标签都分配了不同的图标，如下图所示。  
  
     ![包含随机图标的匹配游戏](../ide/media/express-tut4step3.png "Express_Tut4Step3")  
具有随机图标的匹配游戏  
  
     你没有隐藏这些图标，所以现在可以看到。 若要向玩家隐藏图标，可以将每个标签的 `Forecolor` 属性设置为与 `BackColor` 属性相同的颜色。  
  
    > [!TIP]
    > 隐藏标签等控件的另一种方法是，将其“可见”属性设置为 `False`。  
  
6. 若要隐藏图标，请停止程序并删除 `For Each` 循环内代码注释行上的注释标记。  
  
     [!code-csharp[VbExpressTutorial4Step2_3_4#15](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/cs/form1.cs#15)]
     [!code-vb[VbExpressTutorial4Step2_3_4#15](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/vb/form1.vb#15)]  
  
7. 在菜单栏上，选择“全部保存”按钮保存程序，然后运行该程序。 图标看起来消失了 - 只显示蓝色背景。 但是，图标是随机分配的，仍然存在。 因为图标与背景颜色相同，所以玩家看不到它们。 毕竟，如果玩家能立即看到所有图标，游戏就没有挑战性了！  
  
### <a name="to-continue-or-review"></a>继续或查看  
  
- 要转到下一个教程步骤，请参阅[步骤 4：向每个标签添加一个 Click 事件处理程序](../ide/step-4-add-a-click-event-handler-to-each-label.md)。  
  
- 要返回上一个教程步骤，请参阅[步骤 2：添加随机对象和图标列表](../ide/step-2-add-a-random-object-and-a-list-of-icons.md)。
