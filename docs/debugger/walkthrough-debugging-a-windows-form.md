---
title: 调试 Windows 窗体 |Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], walkthroughs
- debugging managed code, Windows Forms
- debugging [Visual Studio], Windows Forms
- Attach to Process dialog box
- debugger, attaching to programs
- Attach to Process dialog box, walkthroughs
- Windows Forms, debugging
- debugging Windows Forms, walkthroughs
ms.assetid: 529db1e2-d9ea-482a-b6a0-7c543d17f114
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d2f581582acfed38d55a2cfef351856cc0caa945
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65678921"
---
# <a name="walkthrough-debugging-a-windows-form"></a>演练：调试 Windows 窗体
Windows 窗体是最常见的托管应用程序之一。 Windows 窗体创建标准的 Windows 应用程序。 你可以完成此演练使用 Visual Basic 中， C#，或C++。

 首先，您必须关闭任何打开的解决方案。

### <a name="to-prepare-for-this-walkthrough"></a>准备此次演练

- 如果已打开某个解决方案，请将其关闭。 (在**文件**菜单中，选择**关闭解决方案**。)

## <a name="create-a-new-windows-form"></a>创建新的 Windows 窗体
 接下来，您将创建一个新的 Windows 窗体。

#### <a name="to-create-the-windows-form-for-this-walkthrough"></a>若要创建用于本演练中的 Windows 窗体

1. 上**文件**菜单中，选择**新建**然后单击**项目**。

     此时将出现“新建项目”  对话框。

2. 在项目类型窗格中，打开**Visual Basic**， **Visual C#** ，或**Visual C++** 节点，然后

    1. 对于 Visual Basic 或 Visual C# 中，选择**Windows 桌面** > **Windows 窗体应用**。

    2. 视觉对象C++，选择**Windows 桌面应用程序**。

3. 在中**名称**框中，为项目指定唯一名称 (例如，Walkthrough_SimpleDebug)。

4. 单击 **“确定”** 。

     Visual Studio 创建一个新项目，并在 Windows 窗体设计器中显示新窗体。 有关详细信息，请参阅[Windows 窗体设计器](/previous-versions/visualstudio/visual-studio-2010/e06hs424\(v\=vs.100\))。

5. 上**视图**菜单中，选择**工具箱**。

     随即将打开工具箱。 有关详细信息，请参阅[工具箱](../ide/reference/toolbox.md)。

6. 在工具箱中，单击**按钮**控件，将控件拖到窗体设计图面。 将按钮拖动窗体上。

7. 在工具箱中，单击**文本框中**控件，将控件拖到窗体设计图面。 Drop**文本框中**窗体上。

8. 在窗体设计图面上，双击该按钮。

     这会转到代码页。 光标应位于`button1_Click`。

10. 在 `button1_Click` 函数中，添加以下代码：

    ```vb
    textBox1.Text = "Button was clicked!"
    ```

    ```csharp
    textBox1.Text = "Button was clicked!";
    ```

    ```cpp
    textBox1->Text = "Button was clicked!";
    ```

11. 在“生成”菜单上，选择“生成解决方案”   。

     该项目应顺利生成，没有错误。

## <a name="debug-your-form"></a>调试窗体
 现在，已准备好开始调试。

#### <a name="to-debug-the-windows-form-created-for-this-walkthrough"></a>若要调试在本演练中创建的 Windows 窗体

1. 在源窗口中，单击你添加的文本的同一行的左侧的空白：

     ```vb
    textBox1.Text = "Button was clicked!"
    ```

    ```csharp
    textBox1.Text = "Button was clicked!";
    ```

    ```cpp
    textBox1->Text = "Button was clicked!";
    ```

     出现一个红点并且该行上的文本突出显示为红色。 红点表示一个断点。 有关详细信息，请参见[断点](https://msdn.microsoft.com/fe4eedc1-71aa-4928-962f-0912c334d583) 当您在调试器下运行该应用程序时，此调试器将在命中该代码时在该位置中断执行。 然后您可以查看应用程序的状态并调试它。

    > [!NOTE]
    > 此外可以右键单击任意行的代码中，指向**断点**，然后单击**插入断点**该行上添加断点。

2. 在“调试”菜单上选择“启动”   。

     Windows 窗体开始运行。

3. 在 Windows 窗体中，单击添加按钮。

     在 Visual Studio 中，这将转到行上的代码页设置了断点的位置。 该行将用黄色突出显示。 现在，可以查看应用程序中的变量并控制其执行。 你的应用程序现已停止执行，等待您的操作。

4. 上**调试**菜单中，选择**Windows**，然后**观看**，然后单击**Watch1**。

5. 在中**监视 1**窗口中，单击某一空行。 在中**名称**列中，键入`textBox1.Text`(如果使用 Visual Basic 或 Visual C#) 或`textBox1->Text`(如果使用的C++)，然后按 ENTER。

     **监视 1**窗口会显示此变量的值与引号中：

    `""`

6. 在“调试”菜单上选择“逐语句”   。

     TextBox1.Text 的更改的值**监视 1**窗口：

    `Button was clicked!`

7. 上**调试**菜单中，选择**继续**以继续进行调试您的程序。

8. 在 Windows 窗体中，再次单击按钮。

     Visual Studio 将中断再次执行。

9. 单击表示断点的红点。

     这将在代码中移除该断点。

10. 在“调试”菜单上，选择“停止调试”   。

## <a name="attach-to-your-windows-form-application-for-debugging"></a>附加到 Windows 窗体应用程序进行调试
 在 [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] 中，可以将调试器附加到正在运行的进程上。 如果使用 Express Edition，不支持此功能。

#### <a name="to-attach-to-the-windows-form-application-for-debugging"></a>若要将附加到 Windows 窗体应用程序进行调试

1. 在上述步骤中创建的项目中，单击左侧边距处来再一次所添加的行处设置断点：

     ```vb
    textBox1.Text = "Button was clicked!"
    ```

    ```csharp
    textBox1.Text = "Button was clicked!";
    ```

    ```cpp
    textBox1->Text = "Button was clicked!";
    ```

2. 上**调试**菜单中，选择**启动但不调试**。

     Windows 窗体会开始运行 Windows，就像你双击其可执行文件。 未附加调试器。

3. 上**调试**菜单中，选择**附加到进程**。 (此命令，还可以在**工具**菜单。)

     出现 **“附加到进程”** 对话框。

4. 在中**可用进程**窗格中，查找过程中的名称 (Walkthrough_SimpleDebug.exe)**进程**列并单击它。

5. 单击**附加**按钮。

6. 在 Windows 窗体中，单击一个，只有按钮。

     调试器在断点处中断执行的 Windows 窗体。

## <a name="see-also"></a>请参阅
- [调试托管代码](../debugger/debugging-managed-code.md)
- [调试器安全](../debugger/debugger-security.md)
