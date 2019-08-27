---
title: 设置调试和发布配置 |Microsoft Docs
ms.date: 10/05/2018
ms.topic: reference
f1_keywords:
- vs.debug.builds
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- configurations, release
- build configurations, release
- projects [Visual Studio], release configurations
- debugging [Visual Studio], release configurations
- release builds, changing settings
- debug builds
- debug builds, switching to release build
- debug builds, changing configuration settings
- debugging [Visual Studio], debug configurations
- projects [Visual Studio], debug configurations
- build configurations, debug
- debug configurations
- release builds, switching to debug build
- Visual Basic projects, debug and release builds
ms.assetid: 57b6bbb7-f2af-48f7-8773-127d75034ed2
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 75acf0a3a821b4d2561ea14e583e71761b8b476e
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68925479"
---
# <a name="set-debug-and-release-configurations-in-visual-studio"></a>在 Visual Studio 中设置调试和发布配置

Visual Studio 项目具有针对你的程序的单独发布和调试配置。 生成调试版本以进行调试, 并生成最终发布的发布版本。

在调试配置中, 程序将编译为包含完整的符号调试信息, 而不进行优化。 优化会使调试复杂化，因为源代码和生成的指令之间的关系更加复杂。

程序的 "发布" 配置没有任何符号调试信息, 并且已完全优化。 对于托管代码和C++代码, 可以在 .pdb 文件中生成调试信息, 具体取决于所使用[的编译器选项](#BKMK_symbols_release)。 如果以后必须调试发行版本, 创建 .pdb 文件会很有用。

有关生成配置的详细信息，请参阅[了解生成配置](../ide/understanding-build-configurations.md)。

可以从“生成”菜单、从工具栏或在项目的属性页中更改生成配置。 项目属性页是特定于语言的。 下面的过程演示如何从菜单和工具栏更改生成配置。 有关如何在不同语言的项目中更改生成配置的详细信息, 请参阅下面的 "[另请参阅](#see-also)" 部分。

## <a name="change-the-build-configuration"></a>更改生成配置

若要更改生成配置, 请执行以下操作之一:

* 在 "**生成**" 菜单中, 选择 " **Configuration Manager**", 然后选择 "**调试**" 或 "**发布**"。

或

* 在工具栏上，从“解决方案配置”列表选择“调试”或“发布”。

  ![工具栏生成配置](../debugger/media/toolbarbuildconfiguration.png "ToolbarBuildConfiguration")

## <a name="BKMK_symbols_release"></a>为生成生成符号 (.pdb) 文件 (C#、 C++、Visual Basic、) F#

您可以选择生成符号 (.pdb) 文件以及要包含的调试信息。 对于大多数项目类型, 默认情况下, 编译器会为调试版本和发布版本生成符号文件, 而其他默认设置则不同于项目类型和 Visual Studio 版本。

> [!IMPORTANT]
> 调试器只会为可执行文件加载与该可执行文件生成之时所创建的 .pdb 文件完全匹配的 .pdb 文件（即该 .pdb 文件必须是原始 .pdb 文件或其副本）。 有关详细信息, 请参阅[为什么 Visual Studio 要求调试器符号文件与生成它们的二进制文件完全匹配？](https://blogs.msdn.microsoft.com/jimgries/2007/07/06/why-does-visual-studio-require-debugger-symbol-files-to-exactly-match-the-binary-files-that-they-were-built-with/)。

每个项目类型可能有不同的方法来设置这些选项。

### <a name="generate-symbol-files-for-a-c-aspnet-or-visual-basic-project"></a>为C#、ASP.NET 或 Visual Basic 项目生成符号文件

有关或 Visual Basic 中C#调试配置的项目设置的详细信息, 请参阅调试配置的[项目C# ](../debugger/project-settings-for-csharp-debug-configurations.md)设置或[Visual Basic 调试配置的项目设置](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)。

1. 在“解决方案资源管理器”中，选择项目。

2. 选择 "**属性**" 图标 (或按**Alt + enter**)。

3. 在侧窗格中, 选择 "**生成**" (或 "在 Visual Basic 中**编译**"。

4. 在 "**配置**" 列表中, 选择 "**调试**" 或 "**发布**"。

5. 选择 "**高级**" 按钮 (或 Visual Basic) 中的 "**高级编译选项**" 按钮。

6. 在 "**调试信息**" 列表 (或 Visual Basic 中的 "**生成调试信息**" 列表中, 选择 "**完全**"、"**仅限 Pdb**" 或 "**可移植**"。

   可移植的格式是为.NET Core 的最新的跨平台格式。 有关选项的详细信息, 请参阅 "[高级生成设置"C#对话框 ()](../ide/reference/advanced-build-settings-dialog-box-csharp.md)。

   ![ C#为生成生成 pdb](../debugger/media/dbg_project_properties_pdb_csharp.png "GeneratePDBsForCSharp")

7. 生成你的项目。

   编译器将在与可执行文件或主输出文件相同的文件夹中创建符号文件。

### <a name="generate-symbol-files-for-a-c-project"></a>生成C++项目的符号文件

1. 在“解决方案资源管理器”中，选择项目。

2. 选择 "**属性**" 图标 (或按**Alt + enter**)。

3. 在 "**配置**" 列表中, 选择 "**调试**" 或 "**发布**"。

4. 在侧窗格中, 选择 "**链接器 > 调试**", 然后选择 "**生成调试信息**的选项"。

   有关中C++的调试配置的项目设置的详细信息, 请参阅[ C++调试配置的项目设置](../debugger/project-settings-for-a-cpp-debug-configuration.md)。

5. 配置用于**生成程序数据库文件**的选项。

   在大多数C++项目中, 默认值为`$(OutDir)$(TargetName).pdb`, 它将在输出文件夹中生成 .pdb 文件。

   ![ C++为生成生成 pdb](../debugger/media/dbg_project_properties_pdb_cplusplus.png "GeneratePDBsforCPlusPlus")

6. 生成你的项目。

   编译器将在与可执行文件或主输出文件相同的文件夹中创建符号文件。

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 调试器中指定符号 (.pdb) 文件和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)<br/>
- [调试器设置和准备](../debugger/debugger-settings-and-preparation.md)<br/>
- [C++ 调试配置的项目设置](../debugger/project-settings-for-a-cpp-debug-configuration.md)<br/>
- [C# 调试配置的项目设置](../debugger/project-settings-for-csharp-debug-configurations.md)<br/>
- [Visual Basic 调试配置的项目设置](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)<br/>
- [如何：创建和编辑配置](../ide/how-to-create-and-edit-configurations.md)
