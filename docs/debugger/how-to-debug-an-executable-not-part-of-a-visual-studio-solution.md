---
title: 调试不属于 Visual Studio 解决方案的应用
titleSuffix: ''
ms.custom: ''
ms.date: 02/21/2020
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- debugging [Visual Studio], executables
- executable files, importing
- executable files, debugging outside of projects
ms.assetid: 3ea176e8-1ce5-42c4-b7a2-abe3a2765033
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 740af718a2928991d46bedbd6709337b9b20a254
ms.sourcegitcommit: bf2e9d4ff38bf5b62b8af3da1e6a183beb899809
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/22/2020
ms.locfileid: "77557910"
---
# <a name="debug-an-app-that-isnt-part-of-a-visual-studio-solution-c-c-visual-basic-f"></a>调试不属于 Visual Studio 解决方案的应用（C++、 C#、Visual Basic） F#

可能需要调试不属于 Visual Studio 解决方案的应用程序（*.exe*文件）。 它可能是一个[打开的文件夹](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)项目，或者你或其他人可能已经在 Visual Studio 外部创建了该应用程序，或者你从其他位置获得了该应用程序。

- 对于 Visual Studio 中打开的文件夹项目（不包含任何项目或解决方案文件），请参阅[运行和调试代码](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md#run-and-debug-your-code)，或者， C++对于，请[使用启动. 与 json 配置调试参数](/cpp/build/open-folder-projects-cpp#configure-debugging-parameters-with-launchvsjson)。

- 对于 Visual Studio 中不存在的应用程序，调试的常见方法是在 Visual Studio 外部启动该应用程序，然后使用 Visual Studio 调试器中的 "**附加到进程**" 附加到该应用程序。 有关详细信息，请参阅[附加到正在运行的进程](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)。

   附加到应用需要手动步骤，需要花费几秒钟时间。 由于此延迟，附加不会帮助调试启动问题，也不会等待用户输入并快速完成。

   在这些情况下，你可以为应用程序创建 Visual Studio EXE 项目，或者将其导入到C#现有的、Visual Basic C++或解决方案中。 并非所有编程语言都支持 EXE 项目。

>[!IMPORTANT]
>不是在 Visual Studio 中生成的应用程序的调试功能受到限制，无论是附加到应用程序还是将其添加到 Visual Studio 解决方案。
>
>如果有源代码，最佳方法是将代码导入到 Visual Studio 项目中。 然后，运行该应用程序的调试版本。
>
>如果没有源代码，并且应用程序没有兼容格式的[调试信息](../debugger/how-to-set-debug-and-release-configurations.md)，则可用的调试功能非常少。

### <a name="to-create-a-new-exe-project-for-an-existing-app"></a>为现有应用程序创建新的 EXE 项目

1. 在 Visual Studio 中，选择 "**文件**" > **打开**" > **项目**"。

1. 在 "**打开项目**" 对话框中，选择 "**文件名**" 旁边的下拉列表中的 "**所有项目文件**" （如果尚未选中）。

1. 导航到 *.exe*文件，选择它，然后选择 "**打开**"。

   此文件将显示在一个新的临时 Visual Studio 解决方案中。

1. 从 "**调试**" 菜单中选择执行命令（如 "**启动调试**"），开始调试应用程序。

### <a name="to-import-an-app-into-an-existing-visual-studio-solution"></a>将应用导入现有 Visual Studio 解决方案

1. 在 Visual C++Studio C#中打开、或 Visual Basic 解决方案后，选择 "**文件**" > **添加** > **现有项目**。

1. 在 "**打开项目**" 对话框中，选择 "**文件名**" 旁边的下拉列表中的 "**所有项目文件**" （如果尚未选中）。

1. 导航到 *.exe*文件，选择它，然后选择 "**打开**"。

   该文件在当前解决方案中显示为一个新项目。

1. 选择新文件后，从 "**调试**" 菜单中选择执行命令（如 "**启动调试**"），开始调试应用程序。

### <a name="see-also"></a>另请参阅
- [调试器设置和准备](../debugger/debugger-settings-and-preparation.md)
- [调试器安全](../debugger/debugger-security.md)
- [DBG 文件](/previous-versions/visualstudio/visual-studio-2010/da528y14(v=vs.100))