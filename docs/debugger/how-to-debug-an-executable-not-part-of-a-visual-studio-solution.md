---
title: 调试不是 Visual Studio 解决方案的一部分在应用程序
titleSuffix: ''
ms.custom: seodec18
ms.date: 11/19/2018
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
ms.openlocfilehash: 2db4cf8a678b6c20693dcc9c1e730d83f0d5ca7a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62848006"
---
# <a name="debug-an-app-that-isnt-part-of-a-visual-studio-solution-c-c-visual-basic-f"></a>调试的应用程序不是 Visual Studio 解决方案的一部分 (C++， C#，Visual Basic 中， F#)

你可能想要调试应用程序 (*.exe*文件) 的不是 Visual Studio 解决方案的一部分。 你或其他人可能已创建 Visual Studio 外部的应用或从其他位置获取应用程序。

若要调试的应用程序在 Visual Studio 中不存在的常用方法是启动 Visual Studio 外部应用程序，然后附加到使用其**附加到进程**Visual Studio 调试器中。 有关详细信息，请参阅[附加到正在运行的进程](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)。

附加到应用程序需要花费几秒钟的手动步骤。 由于这种延迟，附加将不会有帮助调试的启动问题，或的应用程序不会等待用户输入而迅速完成。

在这些情况下，可以创建应用程序，Visual Studio EXE 项目或将其导入的现有C#，Visual Basic 或C++解决方案。 并非所有编程语言都支持 EXE 项目。

>[!IMPORTANT]
>是否附加到应用或将其添加到 Visual Studio 解决方案，将受到限制，不在 Visual Studio 中生成的应用的调试功能。
>
>如果你有源代码，最好的方法是导入到 Visual Studio 项目中的代码。 然后，运行该应用程序的调试版本。
>
>如果没有源代码，并且此应用没有[调试信息](../debugger/how-to-set-debug-and-release-configurations.md)兼容的格式，在可用的调试功能是非常少。

### <a name="to-create-a-new-exe-project-for-an-existing-app"></a>若要创建现有的应用程序的新 EXE 项目

1. 在 Visual Studio 中，选择**文件** > **打开** > **项目**。

1. 在中**打开项目**对话框中，选择**所有项目文件**，如果尚未选择，请在下拉列表中下一步**文件名**。

1. 导航到 *.exe*文件，选择它，然后选择**打开**。

   该文件将显示在新的临时 Visual Studio 解决方案中。

1. 开始调试此应用，通过选择执行命令，如**开始调试**，从**调试**菜单。

### <a name="to-import-an-app-into-an-existing-visual-studio-solution"></a>若要将应用导入到现有的 Visual Studio 解决方案

1. 使用C++， C#，或 Visual Basic 解决方案打开在 Visual Studio 中，选择**文件** > **添加** > **现有项目**。

1. 在中**打开项目**对话框中，选择**所有项目文件**，如果尚未选择，请在下拉列表中下一步**文件名**。

1. 导航到 *.exe*文件，选择它，然后选择**打开**。

   该文件显示为当前的解决方案下的新项目。

1. 新的文件处于选定状态，开始调试应用程序通过选择执行命令，如**开始调试**，从**调试**菜单。

### <a name="see-also"></a>请参阅
- [调试器设置和准备](../debugger/debugger-settings-and-preparation.md)
- [调试器安全](../debugger/debugger-security.md)
- [DBG 文件](/previous-versions/visualstudio/visual-studio-2010/da528y14(v=vs.100))