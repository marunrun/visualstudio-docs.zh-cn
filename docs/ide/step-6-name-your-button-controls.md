---
title: 步骤 6：命名按钮控件
ms.date: 08/30/2016
ms.assetid: 56b3baa3-651e-4ad4-8942-e334c5c57158
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
dev_langs:
- CSharp
- VB
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a5c23f48e803665e00155d1b546ace4e4ec7bc54
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "77579790"
---
# <a name="step-6-name-your-button-controls"></a>步骤 6：命名按钮控件

窗体上只有一个 <xref:System.Windows.Forms.PictureBox>。 当添加此控件时，IDE 自动将其命名为“pictureBox1”  。 只有一个名为“checkBox1”  的 <xref:System.Windows.Forms.CheckBox>。 很快，你将编写一些代码，并且这些代码将引用到 CheckBox 和 PictureBox。 因为上述每种控件都只有一个控件，所以当你在代码中看到“pictureBox1”或“checkBox1”时，应知道其中的含义   。

> [!TIP]
> 在 Visual Basic 中，任何控件名称的第一个字母默认是首字母大写，因此名称为 **“PictureBox1”** 、 **“CheckBox1”** 等等。

窗体上包含四个按钮，IDE 将它们分别命名为“button1”  、“button2”  、“button3”  和  “button4”。 只看这些按钮的当前名称，你并不知道哪个按钮是“关闭”  按钮，哪个按钮是“显示图片”  按钮。 这就是为按钮控件提供包含更多信息的名字会很有帮助的原因。

## <a name="to-name-your-button-controls"></a>要命名按钮控件

1. 在窗体上，选择“关闭”  按钮。 （如果你仍选择了所有按钮，请选择 Esc  键取消选择。）在“属性”窗口中滚动，直到看到“(Name)”属性。   （当属性按字母顺序排列时，  “(Name)”属性位于顶部附近。）如下面的屏幕截图所示，将此名称更改为“closeButton”  。

    ![带有 closeButton 名称的“属性”窗口](../ide/media/express_setnameproperty.png)<br>带有“closeButton”名称的“属性”窗口   

    > [!NOTE]
    > 尝试将按钮的名称更改为“close Button”，单词“close”和“Button”之间有一个空格  。 当你执行此操作时，IDE 会显示错误消息：“属性值无效。” 控件名称中不允许使用空格和一些其他字符。

1. 将其他三个按钮重命名为“backgroundButton”  、  “clearButton”和“showButton”  。
你可通过选择“属性”  窗口中的控件选择器下拉列表来验证这些名称。 新的按钮名称将出现。

1. 双击窗体上的“显示图片”  按钮。 或者，选择窗体上的“显示图片”按钮，然后按 Enter 键   。 当你执行此操作时，IDE 将在名为“Form1.cs”的主窗口中打开一个附加选项卡  。 （如果使用的是 Visual Basic，则该选项卡名为“Form1.vb”  ）。

   此选项卡将显示窗体后面的代码文件，如下面的屏幕截图所示。

    ![包含 Visual C&#35; 代码的 Form1.cs 选项卡](../ide/media/express_showbuttoncode.png)<br>
包含 C# 代码的“Form1.cs”选项卡 

    > [!NOTE]
    > Form1.cs 或 Form1.vb 选项卡可能会将“showButton”改为显示为“ShowButton”   。

1. 重点考虑这一部分的代码。

    ```csharp
        private void ShowButton_Click(object sender, EventArgs e)
    {
    }
    ```

    ```vb
        Private Sub showButton_Click() Handles showButton.Click

    End Sub
    ```

   [!INCLUDE [devlang-control-csharp-vb](./includes/devlang-control-csharp-vb.md)]

   你正在查看名为 `showButton_Click()`（或者 `ShowButton_Click()`）的代码。 当你打开“showButton”  按钮的代码文件时，IDE 已将此代码添加到窗体的代码中。 在设计时，当你打开窗体中的某个控件的代码文件时，如果该控件没有代码，则将为该控件生成代码。 运行应用并选择控件（在本例中为“显示图片”按钮）时，该代码（称为“方法”）将会运行   。

1. 再次选择“Windows 窗体设计器”选项卡（“Form1.cs [设计]”），然后打开“清除图片”按钮的代码文件以在窗体的代码中为它创建方法    。 对于剩余两个按钮，重复此操作。 IDE 每次都会向窗体的代码文件添加一个新方法。

1. 若要再添加一个方法，请在“Windows 窗体设计器”  中打开 CheckBox  控件的代码文件，以使 IDE 添加 `checkBox1_CheckedChanged()` 方法。 每当用户选中或清除此复选框时都将调用此方法。

   > [!TIP]
   > 运行应用时，经常要在代码编辑器和 Windows 窗体设计器之间进行移动  。 有了 IDE，就能够轻松地在项目中导航。 使用“解决方案资源管理器”通过双击 C# 中的“Form1.cs”或 Visual Basic 中的“Form1.vb”打开“Windows 窗体设计器”，或者在菜单栏上选择“视图” > “设计器”       。

    下面显示了你在代码编辑器中看到的新代码。

    [!code-csharp[VbExpressTutorial1Step6_#2](../ide/codesnippet/CSharp/step-6-name-your-button-controls_2.cs)]

    [!code-vb[VbExpressTutorial1Step6_#2](../ide/codesnippet/VisualBasic/step-6-name-your-button-controls_2.vb)]

    > [!NOTE]
    > 代码可能未使用 camelCase 字母形式显示事件处理程序。

    你所添加的五个方法称为“事件处理程序”，原因是每当事件（如用户选择按钮或选择框）发生时应用程序都将调用这些方法  。

    当你在设计时查看 IDE 中的控件代码时，如果不存在该控件代码，则 Visual Studio 将为控件添加事件处理程序方法。 例如，双击某个按钮时，IDE 将为此按钮的 <xref:System.Windows.Forms.Control.Click> 事件（每当用户选择此按钮时调用）添加一个事件处理程序。 当双击某个复选框时，IDE 会为此复选框的 <xref:System.Windows.Forms.CheckBox.CheckedChanged> 事件（每当用户选中或清除框时调用）添加一个事件处理程序。

    在为控件添加事件处理程序后，通过双击控件或在菜单栏上选择“视图”   > “代码”  ，可以随时从“Windows 窗体设计器”  返回到控件。

    生成程序时名称很重要，并且方法（包括事件处理程序）可以具有任何所需的名称。 使用 IDE 添加事件处理程序时，IDE 将基于控件的名称和正在处理的事件创建一个名称。

    例如，名为“showButton”的按钮的 Click 事件称为 `showButton_Click()`（或者 `ShowButton_Click()`）事件处理程序方法  。 此外，通常会在方法名称后面添加一对括号 `()`，以表明正在讨论的对象是方法。

    如果决定要更改代码的变量名，请右键单击代码中的变量，然后选择“重构”   > “重命名”  。 将重命名代码中变量的所有实例。 有关更多信息，请参阅[重命名重构](../ide/reference/rename.md)。

## <a name="next-steps"></a>后续步骤

* 要转到下一个教程步骤，请参阅[步骤 7：  向窗体添加对话框组件](../ide/step-7-add-dialog-components-to-your-form.md)。

* 要返回上一个教程步骤，请参阅[步骤 5：向窗体添加控件](../ide/step-5-add-controls-to-your-form.md)。

## <a name="see-also"></a>请参阅

* [教程 2：创建计时数学测验](tutorial-2-create-a-timed-math-quiz.md)
* [教程 3：创建匹配游戏](tutorial-3-create-a-matching-game.md)
