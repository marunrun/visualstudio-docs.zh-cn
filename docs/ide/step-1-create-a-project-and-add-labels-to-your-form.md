---
title: 步骤 1：创建项目并向窗体添加标签
ms.date: 10/15/2019
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.assetid: f44e50be-a5f5-4d77-9cff-dd52374c3f74
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9e8e306aea1615649223c96f0c5a7041574f844d
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75588845"
---
# <a name="step-1-create-a-project-and-add-labels-to-your-form"></a>步骤 1：创建项目并向窗体添加标签

在开发此测验的过程中，首先应创建项目并将数个标签、一个按钮和其他控件添加到窗体。 此外还要设置已添加各个控件的属性。 项目将包含窗体、控件和代码（在本教程下文中）。 按钮用于启动测验，标签用于显示测验问题，其他控件则用于显示测验答案和完成测验所剩时间。

> [!NOTE]
> 本主题是基本编码概念教程系列中的一部分。 
> - 有关本教程的概述，请参阅[教程 2：创建计时数学测验](../ide/tutorial-2-create-a-timed-math-quiz.md)。 
> - 若要下载完整版代码，请参阅[数学测验教程的完整示例](https://code.msdn.microsoft.com/Complete-Math-Quiz-8581813c)。

## <a name="to-create-a-project-for-a-form"></a>为窗体创建项目

::: moniker range="vs-2017"

1. 在菜单栏上，依次选择“文件”  >“新建”  >“项目”  。

1. 在“新建项目”  对话框的左侧，选择 Visual C#  或 Visual Basic  ，然后选择“Windows 桌面”  。

1. 在模板列表中，选择“Windows 窗体应用(.NET Framework)”  模板，将其命名为“MathQuiz”  ，然后选择“确定”  按钮。

    此时将显示名为“Form1.cs”或“Form1.vb”的窗体，具体取决于所选择的编程语言。  

   > [!NOTE]
   > 如果没有看到“Windows 窗体应用(.NET Framework)”模板，请使用 Visual Studio 安装程序安装“.NET 桌面开发”工作负载   。<br/><br/>![Visual Studio 安装程序中的 .NET 桌面开发工作负载](../ide/media/dot-net-desktop-dev-workload.png)<br/><br/> 有关详细信息，请参阅[安装 Visual Studio](../install/install-visual-studio.md) 页面。

::: moniker-end

::: moniker range="vs-2019"

1. 在“开始”窗口上，选择“创建新项目”  。

   ![查看“创建新项目”窗口](../get-started/media/vs-2019/create-new-project-dark-theme.png)

1. 在“创建新项目”  窗口的搜索框中输入或键入“Windows 窗体”  。 接下来，从“项目类型”列表中选择“桌面”   。

   应用“项目类型”筛选器之后，为 C# 或 Visual Basic 选择“Windows 窗体应用(.NET Framework)”模板，然后选择“下一步”    。

   ![为“Windows 窗体应用 (.NET Framework)”选择 C# 或 Visual Basic 模板](./media/create-new-project-search-winforms-filtered.png)

   > [!NOTE]
   > 如果未看到“Windows 窗体应用(.NET Framework)”  模板，则可以通过“创建新项目”  窗口安装该模板。 在“找不到所需内容?”消息中，选择“安装更多工具和功能”链接   。
   >
   > ![“创建新项目”窗口内“找不到所需内容”消息中的“安装更多工具和功能”链接](../get-started/media/vs-2019/not-finding-what-looking-for.png)
   >
   > 接下来，在 Visual Studio 安装程序中，选择“.NET 桌面开发”  工作负载。
   >
   > ![Visual Studio 安装程序中的 .NET Core 开发工作负载](../ide/media/install-dot-net-desktop-env.png)
   >
   > 之后，在 Visual Studio 安装程序中选择“修改”按钮  。 系统可能会提示你保存所有内容；如果出现提示，请按照指示进行操作。 接下来，选择“继续”，以安装工作负载  。

1. 在“配置新项目”  窗口中，在“项目名称”  框中键入或输入“MathQuiz”  。 然后，选择“创建”  。

::: moniker-end

## <a name="to-set-properties-for-a-form"></a>设置窗体属性

1. 在 Visual Studio 中，选择窗体（Form1.cs  或 Form1.vb  ，具体取决于编程语言），然后将其“Text”  属性更改为“Math Quiz”  。

     “属性”窗口包含窗体的各个属性。 

1. 将窗体大小更改为 500 像素（宽）× 400 像素（高）。

     您可通过拖动窗体边缘来调整其大小，直到集成开发环境 (IDE) 的左下角显示正确的大小。 或者，你也可以更改“Size”属性的值。 

1. 将“FormBorderStyle”属性的值更改为“Fixed3D”，并将“MaximizeBox”属性设置为“False”。    

     这些值用于防止测验对象改变窗体大小。

## <a name="to-create-the-time-remaining-box"></a>创建“剩余时间”框

1. 从“工具箱”  中添加一个 <xref:System.Windows.Forms.Label> 控件，然后将其“(Name)”  属性的值设置为“timeLabel”  。

     此标签将变成右上角的一个框，其中显示测验的剩余秒数。

2. 将“AutoSize”属性更改为“False”，这样便可以自行调整框的大小。  

3. 将“BorderStyle”属性更改为“FixedSingle”以在框的周围绘制线条。  

4. 将“Size”属性设置为“200, 30”。  

5. 将该标签移到窗体的右上角，此处将显示蓝色分隔线。

     这些分隔线可以帮助您在窗体上对齐控件。

6. 在“属性”  窗口中，选择“Text”  属性，然后选择 Backspace  键以清除此属性的值。

7. 选择“Font”  属性旁边的加号 (+  )，然后将“Size”  属性的值更改为“15.75”  。

     可更改多个字体属性，如以下屏幕截图所示。

     ![显示字号的“属性”窗口](../ide/media/express_setfontsize.png)

8. 从“工具箱”  中再添加一个“标签”控件，然后将其字号设置为“15.75”  。

9. 将“Text”属性设置为“剩余时间”。  

10. 移动该标签，使之整齐排列在“timeLabel”标签的左侧。 

### <a name="to-add-controls-for-the-addition-problems"></a>添加加法题的控件

1. 从“工具箱”  中添加一个“标签”控件，然后将其“Text”  属性设置为“?”  （问号）。

2. 将“AutoSize”属性设置为“False”。  

3. 将“Size”属性设置为“60, 50”。  

4. 将字号设置为“18”。 

5. 将“TextAlign”属性设置为“MiddleCenter”。  

6. 将“Location”属性设置为“50, 75”，以便将此控件置于窗体上。  

7. 将“(Name)”属性设置为“plusLeftLabel”。  

8. 选择“plusLeftLabel”  标签，然后选择 Ctrl  +C  键或“编辑”  菜单上的“复制”  。

9. 通过选择 Ctrl  +V  键或“编辑”  菜单上的“粘贴”  ，将此标签粘贴三次。

10. 排列这三个新标签，使之在“plusLeftLabel”标签的右侧排成一行。 

     您可以使用分隔线将它们隔开并将它们排成一行。

11. 将第二个标签的“Text”属性值设置为 **+** （加号）。 

12. 将第三个标签的“(Name)”属性值设置为“plusRightLabel”。  

13. 将第四个标签的“Text”属性值设置为 **=** （等于号）。 

14. 从“工具箱”  添加一个 <xref:System.Windows.Forms.NumericUpDown> 控件，将其字号设置为“18”  ，并将其宽度设置为“100”  。

     稍后您将了解到有关此类控件的详细信息。

15. 将此“NumericUpDown”控件与加法题的各 Label 控件排成一行。

16. 将“NumericUpDown”控件的“(Name)”  属性值更改为“sum”  。

     如下图所示，你已创建了第一行。

     ![数学测验的第一行](../ide/media/express_firstrow.png)

## <a name="to-add-controls-for-the-subtraction-multiplication-and-division-problems"></a>添加减法、乘法和除法题的控件

1. 复制加法题的全部五个控件（四个 Label 控件和一个 NumericUpDown 控件），然后粘贴这些控件。

     此窗体包含五个新控件，它们仍处于选中状态。

2. 将所有控件移至某处，使之在加法控件的下方排成一行。

     您可以使用分隔线在两行之间留出足够的距离。

3. 将第二个标签的“Text”属性值更改为“-”（减号）   。

4. 将第一个问号标签命名为“minusLeftLabel”。 

5. 将第二个问号标签命名为“minusRightLabel”。 

6. 将“NumericUpDown”控件命名为“difference”  。

7. 将这五个控件再粘贴两次。

8. 在第三行中，将第一个标签命名为“timesLeftLabel”，将第二个标签的“Text”属性更改为“×”（乘号），将第三个标签命名为“timesRightLabel”，然后将 NumericUpDown 控件命名为“product”。     

9. 在第四行中，将第一个标签命名为“dividedLeftLabel”，将第二个标签的“Text”属性更改为“÷”（除号），将第三个标签命名为“dividedRightLabel”，然后将 NumericUpDown 控件命名为“quotient”。     

    > [!NOTE]
    > 您可以复制本教程中的乘号 × 和除号 ÷，将它们粘贴到窗体中。

## <a name="to-add-a-start-button-and-set-the-tab-index-order"></a>添加“开始”按钮并设置 Tab 键索引顺序

1. 从“工具箱”  添加一个 <xref:System.Windows.Forms.Button> 控件，然后将其“(Name)”  属性设置为“startButton”  。

2. 将“Text”属性设置为“开始测验”。  

3. 将字号设置为“14”。 

4. 将“AutoSize”属性设置为“True”，这可使此按钮自动调整大小以适合文本。  

5. 将此按钮置于窗体底部附近的中心位置。

6. 将“startButton”控件的“TabIndex”属性值设置为“1”。   

    > [!NOTE]
    > “TabIndex”  属性用于设置测验对象选择 Tab  键时的控件顺序。 若要查看其工作原理，请打开任何对话框（例如，在菜单栏上，依次选择“文件”   > “打开”  ），然后选择几次 Tab  键。 观察每次选择 Tab  键时，光标是如何从一个控件移动到另一个控件的。 程序员在创建该窗体时便已确定这一顺序。

7. 将 NumericUpDown sum 控件的“TabIndex”属性值设置为“2”，将 difference 控件的此属性值设置为“3”，将 product 控件的此属性值设置为“4”，将 quotient 控件的此属性值设置为“5”。     

     窗体应如以下屏幕截图所示。

     ![初始数学测验窗体](../ide/media/express_formlaidout.png)

8. 若要验证“TabIndex”  属性是否按照预期运行，请选择 F5  键或选择菜单栏上的“调试”   > “启动调试”  保存并运行程序，然后选择几次 Tab  键。

## <a name="to-continue-or-review"></a>继续或查看

- 要转到下一个教程步骤，请参阅[步骤 2：创建随机加法题](../ide/step-2-create-a-random-addition-problem.md)  。

- 要返回概述主题，请参阅[教程 2：创建计时数学测验](../ide/tutorial-2-create-a-timed-math-quiz.md)。
