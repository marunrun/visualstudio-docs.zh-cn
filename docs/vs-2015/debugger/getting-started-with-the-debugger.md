---
title: 入门调试程序 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: c763d706-3213-494f-b4d2-990b6e1ec456
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e093abd5e836bcb7ee236979c00d574a07ecfd3d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68202326"
---
# <a name="getting-started-with-the-debugger"></a>调试程序入门
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 调试器在任何语言环境下都易于使用。 下面我们将介绍如何调试一个简单的 C# 程序，但你也可以对使用 C++ 和 JavaScript 等其他语言的代码应用相同的步骤。  
  
## <a name="debug-a-basic-c-project"></a><a name="BKMK_Start_debugging_a_VS_project"></a> 调试基本 c # 项目  
 让我们从一个简单的 c # 控制台应用程序 (**文件/新建/项目**，然后选择 " **Visual c #** "，然后选择 " **控制台应用程序** ") 。 如果之前从未使用过 Visual Studio，请参阅 [演练：创建简单的应用程序](../ide/walkthrough-create-a-simple-application-with-visual-csharp-or-visual-basic.md)。 **Main**方法只是将1添加到整数变量10次，并将结果输出到控制台：  
  
```csharp  
static void Main(string[] args)  
{  
    int testInt = 0;  
    for (int i = 1; i <= 10; i++)  
    {  
        testInt += 1;  
    }  
    Console.WriteLine(testInt);  
}  
```  
  
 在 **调试** 配置中生成此代码。 默认情况下已设置此配置。 有关配置的详细信息，请参阅 [了解生成配置](../ide/understanding-build-configurations.md)。  
  
 通过单击 " **调试"/"启动调试** " (或工具栏上的 " **启动** "，或按 **F5**) 在调试器中运行此代码。 该应用程序应几乎立即退出，因此实际上无法判断“控制台”窗口中是否打印了任何内容。  
  
 你可以停止执行足够长的时间以查看“控制台”窗口，方法是设置一个断点然后单步前进。 若要设置断点，请将光标放在 `Console.WriteLine` 行中，单击 "调试" **/"新建断点/函数断点**"，或只需在同一行的左边距中单击。 断点应如下所示：  
  
 ![设置断点](../debugger/media/getstartedbreakpoint.png "GetStartedBreakpoint")  
  
 有关断点的详细信息，请参阅 [使用断点](../debugger/using-breakpoints.md)。  
  
## <a name="inspect-variables"></a><a name="BKMK_Inspect_Variables"></a> 检查变量  
 调试通常涉及查找不包含你在某个特定点上所需值的变量。 我们将介绍一些可检查变量的方式。  
  
 再次开始调试。 在执行 `Console.WriteLine` 代码之前停止执行。 您可以通过单步执行 (单击 "调试" **/"逐过程** " 或按 **F10**) 来执行该操作。 在这种情况下，您可以选择 " **单步执行** " (**F11**) 并获得相同的结果;稍后我们将对此进行介绍。 具有方法的最后一个大括号的行应已变为黄色。 查看控制台窗口。 应该会看到 **10 个**。  
  
 您可以将鼠标悬停在 **testInt** 变量上，以查看数据提示中的当前值。  
  
 ![DBG&#95;基础知识&#95;数据&#95;提示](../debugger/media/dbg-basics-data-tips.png "DBG_Basics_Data_Tips")  
  
 在代码窗口的正下方应会看到 **"自动"、"****局部变量**" 和 "**监视**" 窗口。 在执行时，这些窗口将显示变量的当前值。 "自动" 和 "**局部变量** **" 窗口**显示的**testInt**值为**10**。  
  
 ![调试时的自动窗口](../debugger/media/getstartedwindows.png "GetStartedWindows")  
  
 有关这些窗口的详细信息，请参阅 "自动" [和 "局部变量" 窗口](../debugger/autos-and-locals-windows.md)。  
  
 我们来看看在逐步完成程序时，变量值如何更改。 在行上设置断点 `testInt += 1;` ，然后重新启动调试。 应会看到 "**局部变量**" 和 "自动 **" 窗口中**的**testInt**为**0**， **i**为**1**。 继续调试 (" **调试"/"继续**"，或在工具栏上 **继续** ，或按 **F5**) ，可以看到 **testInt** 的值更改为 **1**， **2**，依此类推。 当你厌倦了了解这些更改后，请删除断点 (**调试/切换断点**，或在边距) 中单击它，然后继续调试。 如果要删除所有断点，请单击 "**调试"/"删除所有断点**"，或按**CTRL + SHIFT + F9**，然后在询问**是否要删除所有断点**的对话框上单击 **"是**"。  
  
## <a name="stepping-into-and-over-function-calls"></a>单步执行和逐过程执行函数调用  
 您可以 (**单) 步** 执行调试程序中的代码来执行代码，也可以在调试器跳过函数时执行代码， (**逐** 过程) ，以快速执行对 (函数代码仍) 的代码。 可以在同一个调试会话中的两个方法之间切换。  
  
 若要查看 " **单步** 执行" 和 "逐 **过程**" 之间的差异，我们需要添加一个由其他方法调用的方法。 将方法添加到 C# 应用程序，并从 Main 方法中调用该方法。 代码应如下所示：  
  
```csharp  
static void Main(string[] args)  
{  
    Method1();  
    Console.WriteLine("end");  
}  
  
private static void Method1()  
{  
    Console.WriteLine("in Method1");  
}  
```  
  
 在 Main 方法中的 `Method1();` 调用上设置断点并启动调试。 执行中断后，单击工具栏上的 " **调试"/"单步** 执行" (或 " **单步** 执行"，或按 **F11**) 。 执行在 method1 () 中的第一个大括号处再次中断：  
  
 ![单步执行代码](../debugger/media/getstartedstepinto.png "GetStartedStepInto")  
  
 停止调试并再次开始，当执行在断点处中断时，单击工具栏上的 " **调试"/"逐过程** " (或 " **逐过程** "，或按 **F10**) 。 执行在 `Console.WriteLine("end");` 处再次中断。  
  
 如果要了解有关使用调试器导航代码的详细信息，请参阅 [使用调试器浏览代码](../debugger/navigating-through-code-with-the-debugger.md)。
