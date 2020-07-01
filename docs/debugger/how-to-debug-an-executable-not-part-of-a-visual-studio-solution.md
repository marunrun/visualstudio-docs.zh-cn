---
title: 调试不属于 Visual Studio 解决方案的应用
titleSuffix: ''
ms.custom: ''
ms.date: 02/21/2020
ms.topic: how-to
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
ms.openlocfilehash: c8cb71acb9c1c332f269f77129fa2d11a9a874f8
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2020
ms.locfileid: "85350142"
---
# <a name="debug-an-app-that-isnt-part-of-a-visual-studio-solution-c-c-visual-basic-f"></a>调试不属于 Visual Studio 解决方案的应用（C++、C#、Visual Basic、F#）

建议调试不属于 Visual Studio 解决方案的应用（.exe 文件）。 它可能是一个“[打开文件夹](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)”项目，或者你或其他人可能在 Visual Studio 之外创建了应用，或者从其他地方获得了应用。

- 有关 Visual Studio 中的打开文件夹项目（不包含项目或解决方案文件），请参阅[运行并调试代码](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md#run-and-debug-your-code)或者，对于 C++，请参阅[使用 launch.vs.json 配置调试参数](/cpp/build/open-folder-projects-cpp#configure-debugging-parameters-with-launchvsjson)。

- 对于 Visual Studio 中不存在的应用，常用的调试方法是：在 Visual Studio 之外启动应用，然后在 Visual Studio 调试器中使用“附加到进程”，附加到该应用。 有关详细信息，请参阅[附加到正在运行的进程](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)。

   附加到应用需要几个手动步骤，这需要几秒钟的时间。 由于此延迟，附加操作不会帮助调试启动问题，也不会调试不等待用户输入并快速完成的应用。

   在这些情况下，可以为应用创建 Visual Studio EXE 项目，或将其导入到现有的 C#、Visual Basic 或 C++ 解决方案中。 并非所有编程语言都支持 EXE 项目。

>[!IMPORTANT]
>无论是附加到应用还是将其添加到 Visual Studio 解决方案，Visual Studio 中未构建的应用的调试功能都会受到限制。
>
>如果有源代码，最好的方法是将代码导入 Visual Studio 项目。 然后，运行该应用的调试版本。
>
>如果没有源代码，并且应用没有[调试信息](../debugger/how-to-set-debug-and-release-configurations.md)兼容格式，则可用的调试功能很少。

### <a name="to-create-a-new-exe-project-for-an-existing-app"></a>为现有的应用创建 EXE 项目

1. 在 Visual Studio 中，选择“文件” > “打开” > “项目”  。

1. 在“打开项目”对话框中，选择“所有项目文件”，如果尚未选择，则在“文件名”旁边的下拉列表中进行选择  。

1. 导航到“.exe”文件，选择它，然后选择“打开”。

   该文件将显示在新的临时 Visual Studio 解决方案中。

1. 通过选择执行命令（例如从“调试”菜单选择“开始调试”）开始调试应用 。

### <a name="to-import-an-app-into-an-existing-visual-studio-solution"></a>将应用导入现有 Visual Studio 解决方案

1. 在 Visual Studio 中打开 C++、C# 或 Visual Basic 解决方案后，选择“文件” > “添加” > “现有项目”  。

1. 在“打开项目”对话框中，选择“所有项目文件”，如果尚未选择，则在“文件名”旁边的下拉列表中进行选择  。

1. 导航到“.exe”文件，选择它，然后选择“打开”。

   该文件在当前解决方案下显示为新项目。

1. 选择新文件后，通过选择执行命令（例如从“调试”菜单选择“开始调试”）开始调试应用 。

### <a name="see-also"></a>请参阅
- [调试器设置和准备](../debugger/debugger-settings-and-preparation.md)
- [调试器安全](../debugger/debugger-security.md)
- [DBG 文件](/previous-versions/visualstudio/visual-studio-2010/da528y14(v=vs.100))