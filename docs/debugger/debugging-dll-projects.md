---
title: 调试 DLL 项目 |Microsoft Docs
ms.date: 11/06/2018
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging DLLs
- templates, debugging DLLs
- DLLs, debugging
- debugging [Visual Studio], DLLs
ms.assetid: 433cab30-d191-460b-96f7-90d2530ca243
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8ec10f226ad139ffbeb46badc6ef3dd6c384af91
ms.sourcegitcommit: 5483e399f14fb01f528b3b194474778fd6f59fa6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66714936"
---
# <a name="debug-dlls-in-visual-studio-c-c-visual-basic-f"></a>调试 Visual Studio 中的 Dll (C#， C++，Visual Basic 中， F#)

DLL （动态链接库） 是包含可被多个程序使用的代码和数据的库。 你可以使用 Visual Studio 创建、 构建、 配置和调试 DLL。

## <a name="create-a-dll"></a>创建一个 DLL

以下 Visual Studio 项目模板可以创建 Dll:

- C#Visual Basic 中，或F#类库
- C#Visual Basic Windows 窗体控件 (WCF) 库或
- C++动态链接库 (DLL)

有关详细信息，请参见 [MFC 调试技术](../debugger/mfc-debugging-techniques.md)。

调试 WCF 库类似于调试类库。 有关详细信息，请参阅[Windows 窗体控件](/dotnet/framework/winforms/controls/index)。

通常从另一个项目中调用 DLL。 调试调用项目时，根据 DLL 配置，可以单步跟踪和调试 DLL 代码。

## <a name="vxtskdebuggingdllprojectschangingdefaultconfigurations"></a> DLL 的调试配置

当你使用 Visual Studio 项目模板创建一个应用程序、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]自动为调试和发布生成配置创建所需的设置。 如有必要，您可以更改这些设置。 有关详细信息，请参阅以下文章：

- [C++ 调试配置的项目设置](../debugger/project-settings-for-a-cpp-debug-configuration.md)
- [C#调试配置的项目设置](../debugger/project-settings-for-csharp-debug-configurations.md)
- [Visual Basic 调试配置的项目设置](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)
- [如何：设置调试和发布配置](../debugger/how-to-set-debug-and-release-configurations.md)

### <a name="set-c-debuggableattribute"></a>设置C++DebuggableAttribute

调试器将附加到C++DLLC++代码必须发出`DebuggableAttribute`。

**若要设置`DebuggableAttribute`:**

1. 在“解决方案资源管理器”中选择该 C++ DLL 项目，然后选择“属性”图标，或右键单击该项目并选择“属性”    。

1. 在**属性**窗格中，在**链接器** > **调试**，为**可调试的程序集**选择**是 (/ ASSEMBLYDEBUG)** 。

有关详细信息，请参阅[/ASSEMBLYDEBUG](/cpp/build/reference/assemblydebug-add-debuggableattribute)。

### <a name="vxtskdebuggingdllprojectsexternal"></a> 设置 C /C++ DLL 文件位置

若要调试外部 DLL，调用项目必须能够找到 DLL、其[.pdb 文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)和 DLL 要求的任何其他文件。 你可以创建一个自定义生成任务将这些文件复制到您的 *\<项目文件夹 > \Debug* 输出文件夹中，也可以手动将文件复制到此位置。

对于 C/C++ 项目，可以在项目属性页中设置标头和 LIB 文件位置，而不必将其复制到输出文件夹。

**若要设置 C/C++ 标头和 LIB 文件位置：**

1. 在**解决方案资源管理器**中选择该 C/C++ DLL 项目，然后选择**属性**图标，或右键单击该项目并选择**属性**。

1. 在顶部**属性**窗格下**配置**，选择**所有配置**。

1. 在 **C/C++**  > **常规** > **附加包含目录** 中，指定具有标头文件的文件夹。

1. 在 **链接器** > **常规** > **附加库目录** 中，指定具有 LIB 文件的文件夹。

1. 在 **链接器** > **输入** > **附加依赖项** 中，指定完整路径和 LIB 文件的文件名。

1. 选择 **确定**。

有关C++项目设置的详细信息，请参阅[属性页 （Visual C++）](/cpp/build/reference/property-pages-visual-cpp)。

## <a name="vxtskdebuggingdllprojectsbuildingadebugversion"></a> 生成调试版本

请确保在开始调试之前生成该 DLL 的调试版本。 若要调试 DLL，调用应用程序必须能够找到其 [.pdb 文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md) 和 DLL 要求的任何其他文件。

可以创建自定义生成任务，将 DLL 文件复制到你的 *\<调用项目文件夹 > \Debug* 输出文件夹中，也可以手动将文件复制到此处。

请确保调用位于正确位置的 DLL。 这似乎是理所当然的，但如果调用应用找到并加载其他不同的 DLL，调试器将永远不会命中你设置的断点。

## <a name="vxtskdebuggingdllprojectswaystodebugthedll"></a> 调试 DLL

不能直接运行 DLL。 它必须由一个应用调用，通常是 *.exe* 文件。 有关详细信息，请参阅[创建和管理 Visual C++ 项目](/cpp/ide/creating-and-managing-visual-cpp-projects)。

若要调试 DLL，你可以[从调用应用开始调试](#vxtskdebuggingdllprojectsthecallingapplication)，或通过指定其调用应用[从 DLL 项目开始调试](how-to-debug-from-a-dll-project.md)。 此外可以使用调试器[即时窗口](#vxtskdebuggingdllprojectstheimmediatewindow)在设计时计算 DLL 函数或方法，而无需使用调用应用。

有关详细信息，请参阅[先来看一下调试器](../debugger/debugger-feature-tour.md)。

### <a name="vxtskdebuggingdllprojectsthecallingapplication"></a> 从调用应用开始调试

调用 DLL 的应用可以是：

- [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 项目中与 DLL 在同一或不同解决方案中的应用。
- 已经在测试或生产计算机上部署且正在运行的现有应用。
- 在 web 中通过 URL 访问。
- 具有嵌入了 DLL 的网页的 Web 应用。

从调用应用程序调试 DLL，你可以：

- 打开调用应用程序项目，并开始通过选择调试**调试** > **开始调试**或按**F5**。

  或

- 附加到测试或生产计算机上已部署且正在运行的应用。 针对网站或 Web 应用中的 DLL 使用此方法。 有关详细信息，请参阅[如何：附加到正在运行的进程](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)。

在开始调试调用应用程序之前，请在 DLL 中设置断点。 请参阅[使用断点](../debugger/using-breakpoints.md)。 DLL 断点命中时，可以单步跟踪代码，观察每个行的操作。 有关详细信息，请参阅[在调试器中浏览代码](../debugger/navigating-through-code-with-the-debugger.md)。

在调试期间，可以使用**模块**窗口验证应用加载的 DLL 和 *.exe* 文件。 若要在调试时打开**模块**窗口，选择**调试** > **窗口** > **模块**。 有关详细信息，请参阅[如何：使用“模块”窗口](../debugger/how-to-use-the-modules-window.md)。

### <a name="vxtskdebuggingdllprojectstheimmediatewindow"></a> 使用即时窗口

你可以使用**即时**窗口，以在设计时计算 DLL 函数或方法。 **即时**窗口充当调用应用的角色。

>[!NOTE]
>大多数类型的项目可以在设计时使用**即时**窗口。 它不支持 SQL、 web 项目或脚本。

例如，若要在 `Class1` 类中测试名为 `Test` 的方法:

1. 打开 DLL 项目， 通过选择**调试** > **窗口** > **即时**或按**Ctrl**+**Alt**+**I** 打开 **即时** 窗口。

1. 在 **即时**窗口中键入以下 C# 代码并按**Enter**，以实例化`Class1`类型的对象。 此托管代码也适用于 C# 和 Visual Basic，只需进行合适的语法更改：

   ```csharp
   Class1 obj = new Class1();
   ```

   在 C# 中，所有名称必须是全限定名称。 语言服务尝试计算表达式的值时，所有使用的方法或变量必须在当前作用域和上下文中。

1. 假设 `Test` 带有一个 `int` 参数，使用 **即时** 窗口计算 `Test` ：

   ```csharp
   ?obj.Test(10);
   ```

   结果输出到 **即时** 窗口中。

1. 你可以放置一个断点在 `Test` 方法内继续调试，然后再次计算函数。

   命中断点后，可以单步跟踪`Test`。 `Test` 执行后，调试器将回到设计模式。

## <a name="vxtskdebuggingdllprojectsmixedmodedebugging"></a>混合模式调试

可以为托管或本机代码中的 DLL 编写调用应用。 如果本机应用调用托管 DLL，并且你想要调试两者，则可以在项目属性中同时启用托管和本机调试器。 确切流程取决于是要从 DLL 项目还是从调用应用项目开始调试。 有关详细信息，请参阅[如何：在混合模式下调试](../debugger/how-to-debug-in-mixed-mode.md)。

此外可以调试托管的调用项目中的本机 DLL。 有关详细信息，请参阅[如何调试托管和本机代码](how-to-debug-managed-and-native-code.md)。

## <a name="see-also"></a>请参阅
- [调试托管代码](../debugger/debugging-managed-code.md)
- [Visual C++ 项目类型](../debugger/debugging-preparation-visual-cpp-project-types.md)
- [C#、F# 和 Visual Basic 项目类型](../debugger/debugging-preparation-csharp-f-hash-and-visual-basic-project-types.md)
- [C++ 调试配置的项目设置](../debugger/project-settings-for-a-cpp-debug-configuration.md)
- [C# 调试配置的项目设置](../debugger/project-settings-for-csharp-debug-configurations.md)
- [Visual Basic 调试配置的项目设置](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)
- [调试器安全](../debugger/debugger-security.md)
