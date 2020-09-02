---
title: 演练：调试 Windows 窗体 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
- VB
- CSharp
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
caps.latest.revision: 31
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a553f77e352b16ba1a0709e13e8893cf0f57a43d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65704901"
---
# <a name="walkthrough-debugging-a-windows-form"></a>演练：调试 Windows 窗体
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Windows 窗体是最常见的托管应用程序之一。 Windows 窗体可创建标准的 Windows 应用程序。 可以使用 Visual Basic、C# 或 C++ 来完成本演练。  
  
 首先，必须关闭所有已打开的解决方案。  
  
### <a name="to-prepare-for-this-walkthrough"></a>准备此次演练  
  
- 如果你已经打开了一个解决方案，请先将其关闭。 （在“文件”菜单上，选择“关闭解决方案”。 ）  
  
## <a name="create-a-new-windows-form"></a>创建新的 Windows 窗体  
 接下来，你将创建新的 Windows 窗体。  
  
#### <a name="to-create-the-windows-form-for-this-walkthrough"></a>为本演练创建 Windows 窗体  
  
1. 从“文件”菜单中选择“新建”，然后单击“项目”  。  
  
     此时将出现“新建项目”对话框。  
  
2. 在“项目类型”窗格中，打开 Visual Basic、Visual C# 或 Visual C++ 节点，然后    
  
    1. 对于 Visual Basic 或 Visual c #，请选择 " **windows** " 节点，然后在 "**模板**" 窗格中选择 " **windows 窗体应用程序**"。  
  
    2. 对于 "Visual C++"，请选择 " **CLR** " 节点，然后在 "**模板**" 窗格中选择 " **Windows 窗体应用程序**"。  
  
3. 在“模板”窗格中，选择“Windows 应用程序”。   
  
4. 在“名称”框中，为项目指定唯一的名称（例如 Walkthrough_SimpleDebug）。  
  
5. 单击 **“确定”** 。  
  
     Visual Studio 会创建新项目并在 Windows 窗体设计器中显示新窗体。 有关详细信息，请参阅 [Windows 窗体设计器](https://msdn.microsoft.com/3c3d61f8-f36c-4d41-b9c3-398376fabb15)。  
  
6. 在“视图”菜单中选择“工具箱” 。  
  
     随即将打开工具箱。 有关详细信息，请参阅[工具箱](../ide/reference/toolbox.md)。  
  
7. 在“工具箱”中，单击“按钮”控件，并将该控件拖到窗体设计图面上。 在窗体上放置按钮。  
  
8. 在“工具箱”中，单击“文本框”控件，并将该控件拖到窗体设计图面上。 在窗体上放置“文本框”。  
  
9. 在窗体设计图面上，双击按钮。  
  
     随即将转到代码页。 光标应位于 `button1_Click`。  
  
10. 在 `button1_Click` 函数中，添加以下代码：  
  
    ```  
    ' Visual Basic  
    textBox1.Text = "Button was clicked!"  
  
    // C#  
    textBox1.Text = "Button was clicked!";  
  
    // C++  
    textBox1->Text = "Button was clicked!";  
    ```  
  
11. 在“生成”菜单上，选择“生成解决方案” 。  
  
     该项目应顺利生成，没有错误。  
  
## <a name="debug-your-form"></a>调试窗体  
 现在，你可以开始调试了。  
  
#### <a name="to-debug-the-windows-form-created-for-this-walkthrough"></a>调试为本演练创建的 Windows 窗体  
  
1. 在源窗口中，单击所添加文本所在行的左侧边距：  
  
    ```  
    ' Visual Basic  
    textBox1.Text = "Button was clicked!"  
  
    // C#  
    textBox1.Text = "Button was clicked!";  
  
    // C++  
    textBox1->Text = "Button was clicked!";  
    ```  
  
     出现一个红点并且该行上的文本突出显示为红色。 红点表示一个断点。 有关详细信息，请参见[断点](https://msdn.microsoft.com/fe4eedc1-71aa-4928-962f-0912c334d583) 当您在调试器下运行该应用程序时，此调试器将在命中该代码时在该位置中断执行。 然后您可以查看应用程序的状态并调试它。  
  
    > [!NOTE]
    > 还可以右键单击任意代码行，指向“断点”，然后单击“插入断点”在该行上添加断点 。  
  
2. 在“调试”菜单上选择“启动” 。  
  
     Windows 窗体将开始运行。  
  
3. 在 Windows 窗体上，单击添加的按钮。  
  
     在 Visual Studio 中，执行此操作将转到代码页上设置了断点的行上。 该行将用黄色突出显示。 现在，可以查看应用程序中的变量并控制其执行。 应用程序现在已停止执行，等待你执行操作。  
  
4. 在“调试”菜单上选择“窗口”，然后选择“监视”，再单击“监视 1”   。  
  
5. 在“监视 1”窗口中，单击空行。 在 " **名称** " 列中， `textBox1.Text` 如果使用的是 Visual Basic、Visual c # 或 j # ) 或 `textBox1->Text` (（如果使用的是 c + +) ），请键入 (，然后按 enter。  
  
     “监视 1”窗口将在引号中显示此变量的值，如下所示：  
  
    ```  
    ""  
    ```  
  
6. 在“调试”菜单上选择“逐语句” 。  
  
     textBox1.Text 的值在“监视 1”窗口中更改为：  
  
    ```  
    Button was clicked!  
    ```  
  
7. 在“调试”菜单上，选择“继续”以继续调试程序 。  
  
8. 在 Windows 窗体上，再次单击按钮。  
  
     Visual Studio 将再次中断执行。  
  
9. 单击表示断点的红点。  
  
     这将从代码中移除该断点。  
  
10. 在“调试”菜单上，选择“停止调试” 。  
  
## <a name="attach-to-your-windows-form-application-for-debugging"></a>附加到 Windows 窗体应用程序进行调试  
 在 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 中，可以将调试器附加到正在运行的进程上。 如果使用速成版，则不支持此功能。  
  
#### <a name="to-attach-to-the-windows-form-application-for-debugging"></a>附加到 Windows 窗体应用程序进行调试  
  
1. 在上面创建的项目中，单击左边距再次在添加的行上设置断点：  
  
    ```  
    ' Visual Basic  
    textBox1.Text = "Button was clicked!"  
  
    // C#  
    textBox1.Text = "Button was clicked!"  
  
    // C++  
    textBox1->Text = "Button was clicked!";  
    ```  
  
2. 在“调试”菜单中，选择“启动但不调试” 。  
  
     Windows 窗体在 Windows 下开始运行，就像双击了它的可执行文件一样。 调试器未附加。  
  
3. 在“调试”菜单上，选择“附加到进程” 。 （在“工具”菜单上也可找到此命令）。  
  
     出现 **“附加到进程”** 对话框。  
  
4. 在“可用进程”窗格的“进程”列中找到进程名称 (Walkthrough_SimpleDebug.exe) 并单击它 。  
  
5. 单击“附加”按钮。  
  
6. 在 Windows 窗体中，单击仅有的一个按钮。  
  
     调试器在断点处中断 Windows 窗体的执行。  
  
## <a name="see-also"></a>另请参阅  
 [调试托管代码](../debugger/debugging-managed-code.md)   
 [调试器安全](../debugger/debugger-security.md)
