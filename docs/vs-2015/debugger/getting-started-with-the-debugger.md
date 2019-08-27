---
title: 调试器入门 |Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68202326"
---
# <a name="getting-started-with-the-debugger"></a>调试程序入门
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 调试器在任何语言环境下都易于使用。 下面我们将介绍如何调试一个简单的 C# 程序，但你也可以对使用 C++ 和 JavaScript 等其他语言的代码应用相同的步骤。  
  
## <a name="BKMK_Start_debugging_a_VS_project"></a> 调试一个基本 C# 项目  
 让我们先简单 C# 控制台应用程序 (**文件 / 新建 / 项目**，然后选择**Visual C#** ，然后选择**控制台应用程序**)。 如果你从未使用过之前的 Visual Studio，请参阅[演练：创建简单应用程序](../ide/walkthrough-create-a-simple-application-with-visual-csharp-or-visual-basic.md)。 **Main**方法只需将 1 添加到整数变量 10 次，并打印到控制台的结果：  
  
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
  
 生成此代码**调试**配置。 默认情况下已设置此配置。 有关配置的详细信息，请参阅[了解生成配置](../ide/understanding-build-configurations.md)。  
  
 在调试器中运行此代码，通过单击**调试 / 启动调试**(或**启动**的工具栏上，或**F5**)。 该应用程序应几乎立即退出，因此实际上无法判断“控制台”窗口中是否打印了任何内容。  
  
 你可以停止执行足够长的时间以查看“控制台”窗口，方法是设置一个断点然后单步前进。 若要设置断点，请将光标放`Console.WriteLine`行，然后单击**调试 / 新断点 / 函数断点**，或只需单击同一行的左边距。 断点应如下所示：  
  
 ![设置断点](../debugger/media/getstartedbreakpoint.png "GetStartedBreakpoint")  
  
 有关断点的详细信息，请参阅[使用断点](../debugger/using-breakpoints.md)。  
  
## <a name="BKMK_Inspect_Variables"></a> 检查变量  
 调试通常涉及到查找不包含预期的特定点的值的变量。 我们将介绍几种您可以检查变量。  
  
 再次开始调试。 在执行 `Console.WriteLine` 代码之前停止执行。 您可能会导致它执行通过单步前进 (单击**调试 / 单步 Over**或**F10**)。 在这种情况下你可能已选择**单步执行**(**F11**) 并获得相同的结果; 我们稍后将介绍不同之处。 具有方法的最后一个大括号的行应已变为黄色。 查看控制台窗口。 应会看到**10**。  
  
 你可以悬停**testInt**变量以查看数据提示中的当前值。  
  
 ![DBG&#95;Basics&#95;Data&#95;Tips](../debugger/media/dbg-basics-data-tips.png "DBG_Basics_Data_Tips")  
  
 正下方的代码窗口应会看到**自动**，**局部变量**，并**观看**windows。 在执行时，这些窗口将显示变量的当前值。 这两个**自动**并**局部变量**windows 显示**testInt**值为**10**。  
  
 ![自动窗口进行调试时](../debugger/media/getstartedwindows.png "GetStartedWindows")  
  
 有关这些窗口的详细信息，请参阅[自动和局部变量 Windows](../debugger/autos-and-locals-windows.md)。  
  
 我们来看看在逐步完成程序时，变量值如何更改。 上设置断点`testInt += 1;`行，然后重新启动调试。 您应该会看到**testInt**中**局部变量**并**自动**windows 是**0**，和**我**是**1**。 继续调试时 (**调试 / 继续**，或**继续**的工具栏上，或**F5**)，你可以看到的值**testInt**将更改为**1**，然后**2**，依次类推。 当你厌倦了查看这些更改时，删除的断点 (**调试 / 切换断点**，或者在边距中单击)，并继续调试。 如果你想要删除所有断点，请单击**调试 / 删除所有断点**，或**CTRL + SHIFT + F9**，然后单击**是**对话框，询问在**是否要删除所有断点？** .  
  
## <a name="stepping-into-and-over-function-calls"></a>单步执行和逐过程执行函数调用  
 您可以在调试器语句通过-语句中执行代码 (**单步执行**) 或可执行代码，调试器会跳过函数时 (**单步跳过**) 使快速获得您并更感兴趣 （代码函数代码仍被执行）。 您可以在同一个调试会话中这两种方法之间进行切换。  
  
 若要查看之间的差异**单步执行**并**单步跳过**，我们需要添加另一种方法调用的方法。 将方法添加到 C# 应用程序，并从 Main 方法中调用该方法。 代码应如下所示：  
  
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
  
 在 Main 方法中的 `Method1();` 调用上设置断点并启动调试。 执行中断时，单击**调试 / 单步执行**(或**单步执行**的工具栏上，或**F11**)。 执行在 method1 () 中的第一个大括号处再次中断：  
  
 ![单步执行代码](../debugger/media/getstartedstepinto.png "GetStartedStepInto")  
  
 停止调试并再次启动，并执行在断点处中断，单击**调试 / 单步 Over** (或**单步跳过**的工具栏上，或**F10**)。 执行在 `Console.WriteLine("end");` 处再次中断。  
  
 如果你想要了解有关使用调试器导航代码的详细信息，请参阅[使用调试器浏览代码](../debugger/navigating-through-code-with-the-debugger.md)。
