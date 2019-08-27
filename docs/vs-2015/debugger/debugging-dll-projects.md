---
title: 调试 DLL 项目 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging DLLs
- templates, debugging DLLs
- DLLs, debugging
- debugging [Visual Studio], DLLs
ms.assetid: 433cab30-d191-460b-96f7-90d2530ca243
caps.latest.revision: 41
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 4a4533c304f84d9dc59ec6b05328528870e49655
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65691401"
---
# <a name="debugging-dll-projects"></a>调试 DLL 项目
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

以下模板可创建 DLL：  
  
- （C++、C# 和 Visual Basic）：类库  
  
- (C++， C#，和 Visual Basic):Windows 窗体控件库  
  
   调试 Windows 控件库类似于调试类库项目。 大多数情况下将从另一个项目中调用 Windows 控件。 调试调用项目时，可单步执行 Windows 控件的代码，并设置断点，然后执行其他调试操作。 有关详细信息，请参阅 [Windows 窗体控件](https://msdn.microsoft.com/library/f050de8f-4ebd-4042-94b8-edf9a1dbd52a)。  
  
- (C#和 Visual Basic):Web 控件库  
  
   有关更多信息，请参见 [Web Control Library (Managed Code)](../debugger/web-control-library-managed-code.md)。  
  
- (C++):MFC ActiveX 控件和 MFC 智能设备 ActiveX 控件  
  
   ActiveX 控件是可以通过 Internet 下载到客户端计算机，并在网页上显示和激活的控件。  
  
   ActiveX 控件的调试与其他类型的控件的调试类似，因为这些控件都无法独立运行，而且必须嵌入 HTML 网页中。 有关详细信息，请参阅[如何：调试 ActiveX 控件](../debugger/how-to-debug-an-activex-control.md)。  
  
- (C++):MFC 智能设备 DLL  
  
   有关更多信息，请参见 [MFC Debugging Techniques](../debugger/mfc-debugging-techniques.md)。  
  
  本节还包含有关以下主题的信息：  
  
- [如何：从 DLL 项目调试](../debugger/how-to-debug-from-a-dll-project.md)  
  
- [如何：在混合模式下调试](../debugger/how-to-debug-in-mixed-mode.md)  
  
  此主题包含以下几节，这几节提供了有关如何准备调试类库的注意事项：  
  
- [Building a Debug Version](#vxtskdebuggingdllprojectsbuildingadebugversion)  
  
- [Mixed-Mode Debugging](#vxtskdebuggingdllprojectsmixedmodedebugging)  
  
- [Changing Default Configurations](#vxtskdebuggingdllprojectschangingdefaultconfigurations)  
  
- [Ways to Debug the DLL](#vxtskdebuggingdllprojectswaystodebugthedll)  
  
- [The Calling Application](#vxtskdebuggingdllprojectsthecallingapplication)  
  
- [Controls on a Web Page](#vxtskdebuggingdllprojectscontrolsonawebpage)  
  
- [The Immediate Window](#vxtskdebuggingdllprojectstheimmediatewindow)  
  
## <a name="vxtskdebuggingdllprojectsbuildingadebugversion"></a> Building a Debug Version  
 无论如何启动调试，都请首先确保生成 DLL 的调试版本，并确保该调试版本位于应用程序应该能够找到它的位置。 这似乎很明显，但如果忘记这一步骤，应用程序可能会找到并加载 DLL 的其他版本。 然后程序将继续运行，尽管您会奇怪为什么断点从未被命中。 调试时，可以通过打开调试器的 **“模块”** 窗口来检查程序已加载的 DLL。 **“模块”** 窗口列出了所调试进程中加载的每个 DLL 或 EXE。 有关详细信息，请参阅[如何：使用模块窗口](../debugger/how-to-use-the-modules-window.md)。  
  
 为了使调试器附加到用 C++ 编写的代码，该代码必须发出 `DebuggableAttribute`。 可通过链接 [/ASSEMBLYDEBUG](https://msdn.microsoft.com/library/94443af3-470c-41d7-83a0-7434563d7982) 链接器选项将它自动添加到代码中。  
  
## <a name="vxtskdebuggingdllprojectsmixedmodedebugging"></a> Mixed-Mode Debugging  
 调用 DLL 的调用应用程序可以用托管代码编写，也可以用本机代码编写。 如果托管 DLL 由本机代码调用，并且您需要调试两者，则必须同时启用托管调试器和本机调试器。 可以选择在此 **\<项目 > 属性页**对话框或窗口。 具体如何检查取决于是从 DLL 项目中启动调试，还是从调用应用程序项目中启动调试。 有关详细信息，请参阅[如何：在混合模式下调试](../debugger/how-to-debug-in-mixed-mode.md)。  
  
## <a name="vxtskdebuggingdllprojectschangingdefaultconfigurations"></a> Changing Default Configurations  
 用项目模板创建控制台应用程序项目时， [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 将自动为调试和发布配置创建所需的设置。 必要时，可更改这些设置。 有关详细信息，请参阅[的项目设置C++调试配置](../debugger/project-settings-for-a-cpp-debug-configuration.md)，[项目设置为C#调试配置](../debugger/project-settings-for-csharp-debug-configurations.md)，[的 Visual Basic 调试项目设置配置](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)，和[如何：设置调试和发布配置](../debugger/how-to-set-debug-and-release-configurations.md)。  
  
## <a name="vxtskdebuggingdllprojectswaystodebugthedll"></a> Ways to Debug the DLL  
 本节的每个项目都创建一个 DLL。 您无法直接运行 DLL，它必须由应用程序（通常为 EXE）调用。 有关详细信息，请参阅 [Creating and Managing Visual C++ Projects](https://msdn.microsoft.com/library/11003cd8-9046-4630-a189-a32bf3b88047)。 调用应用程序可能满足下列任一条件：  
  
- 内置在同一 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 解决方案中包含类库的另一个项目中的应用程序。  
  
- 已经部署到测试或生产计算机上的现有应用程序。  
  
- 位于 Web 上并通过 URL 访问。  
  
- 包含嵌入了 DLL 的网页的 Web 应用程序。  
  
### <a name="vxtskdebuggingdllprojectsthecallingapplication"></a> 调试调用应用程序  
 若要调试 DLL，请从调试调用应用程序开始，通常是 EXE 或者 Web 应用程序。 调试方式有许多种。  
  
- 如果有调用应用程序的项目，则可以打开该项目并从 **“调试”** 菜单开始执行。 有关详细信息，请参阅[如何：开始执行](https://msdn.microsoft.com/b0fe0ce5-900e-421f-a4c6-aa44ddae453c)。  
  
- 如果调用应用程序是已经部署到测试或生产计算机上并已经运行的现有程序，则可以附加到该应用程序上。 如果 DLL 是由 Internet Explorer 承载的控件或网页上的控件，请使用此方法。 有关详细信息，请参阅[如何：将附加到正在运行的进程](https://msdn.microsoft.com/636d0a52-4bfd-48d2-89ad-d7b9ca4dc4f4)。  
  
- 您可以从 DLL 项目中调试。 有关详细信息，请参阅[如何：调试 DLL 项目从](../debugger/how-to-debug-from-a-dll-project.md)。  
  
- 可以从 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] **“即时”** 窗口中进行调试。 在这种情况下， **“即时”** 窗口充当应用程序的角色。  
  
  在开始调试调用应用程序之前，通常希望在类库中设置一个断点。 有关详细信息，请参阅 [Breakpoints and Tracepoints](https://msdn.microsoft.com/fe4eedc1-71aa-4928-962f-0912c334d583)。 命中断点时，可以逐句通过代码，同时观察每行的操作，直到将问题隔离出来。 有关详细信息，请参阅 [Code Stepping Overview](https://msdn.microsoft.com/8791dac9-64d1-4bb9-b59e-8d59af1833f9)。  
  
### <a name="vxtskdebuggingdllprojectscontrolsonawebpage"></a> Controls on a Web Page  
 若要调试网页控件，请创建嵌入此控件的 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 页（如果尚不存在这样的页）。 然后在网页代码和控件代码中设置断点。 然后从 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]中调用网页。  
  
 在开始调试调用应用程序之前，通常需要在 DLL 中设置一个断点。 命中断点时，可以逐句通过代码，同时观察每行的操作，直到将问题隔离出来。 有关详细信息，请参阅 [Breakpoints and Tracepoints](https://msdn.microsoft.com/fe4eedc1-71aa-4928-962f-0912c334d583)。  
  
### <a name="vxtskdebuggingdllprojectstheimmediatewindow"></a> The Immediate Window  
 可以在没有调用应用程序的情况下计算 DLL 中的函数或方法。 可以进行设计时调试并使用 **“即时”** 窗口。 若要以这种方式进行调试，请在 DLL 项目打开时按照以下步骤操作：  
  
1. 打开调试器 **“即时”** 窗口。  
  
2. 若要测试类 `Test` 中名为 `Class1`的方法，请通过在“即时”窗口中键入以下 C# 代码来实例化类型为 `Class1` 的对象。 对语法进行以下适当更改后，此托管代码对 Visual Basic 和 C++ 有效：  
  
    ```  
    Class1 obj = new Class1();  
    ```  
  
     在 C# 中，所有名称必须是全限定名称。 而且，任何方法或变量都必须处在调试会话的当前范围和上下文中。  
  
3. 假设 `Test` 带有一个 `int` 参数，使用 `Test` “即时” **窗口计算** ：  
  
    ```  
    ?obj.Test(10)  
    ```  
  
     结果将打印在 **“即时”** 窗口中。  
  
4. 您可以继续调试 `Test` ，方法为在其中设置断点然后再次计算函数：  
  
    ```  
    ?obj.Test(10);  
    ```  
  
     断点将被命中，然后您将可以逐步调试 `Test`。 当执行离开 `Test`后，调试器将返回设计模式。  
  
## <a name="see-also"></a>请参阅  
 [调试托管代码](../debugger/debugging-managed-code.md)   
 [Visual C++ 项目类型](../debugger/debugging-preparation-visual-cpp-project-types.md)   
 [C#、F#、和 Visual Basic 项目类型](../debugger/debugging-preparation-csharp-f-hash-and-visual-basic-project-types.md)   
 [C++ 调试配置的项目设置](../debugger/project-settings-for-a-cpp-debug-configuration.md)   
 [C# 调试配置的项目设置](../debugger/project-settings-for-csharp-debug-configurations.md)   
 [Visual Basic 调试配置的项目设置](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)   
 [调试器安全](../debugger/debugger-security.md)
