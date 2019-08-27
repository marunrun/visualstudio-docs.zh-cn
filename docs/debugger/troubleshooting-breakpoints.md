---
title: 在调试器中的断点疑难解答 |Microsoft Docs
ms.custom: seodec18
ms.date: 01/23/2018
ms.topic: troubleshooting
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bbcda5eef8ac6ac6aa20c6f487dfc94beb10866c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62929665"
---
# <a name="troubleshoot-breakpoints-in-the-visual-studio-debugger"></a>在 Visual Studio 调试器中的断点疑难解答

## <a name="breakpoint-warnings"></a>断点警告

断点在调试时，有两个可能的可视状态： 一个实心的红色圆和 （白色填充） 空心圆。 如果调试器能够成功在目标进程中设置断点，它将保持一个实心的红色圆。 如果断点是空心圆，禁用断点，或尝试设置断点时出现警告。 若要确定的不同，断点上悬停并查看是否存在一条警告。

以下两个部分介绍重要警告以及如何解决这些问题。

### <a name="no-symbols-have-been-loaded-for-this-document"></a>“尚未为此文档加载任何符号”

转到**模块**窗口 (**调试** > **Windows** > **模块**) 并检查是否为你的模块加载。
* 如果加载你的模块，则检查**符号状态**列，以查看是否已加载符号。
  * 如果还未加载符号，检查符号状态来诊断问题。 从上下文菜单中的模块上**模块**窗口中，单击**符号加载信息...** 若要查看其中调试器尝试并加载符号。 有关加载符号的详细信息，请参阅[指定符号 (.pdb) 和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)。
  * 如果已加载符号，PDB 不包含有关源文件的信息。 以下是几个可能的原因：
    * 如果最近添加的源文件，确认正在加载的模块的最新版本。
    * 可以创建使用去除的 Pdb **/PDBSTRIPPED**链接器选项。 去除的 Pdb 不包含源文件信息。 确认你正在使用完整 PDB 和不去除的 PDB。
    * PDB 文件部分已损坏。 删除文件，并执行干净的生成的模块来尝试解决此问题。

* 如果你的模块未加载，请检查以下内容来查找原因：
  * 确认您正在调试的正确过程。
  * 请检查你正在调试的代码正确的类型。 您可以了解哪种代码将调试器配置为在调试**进程**窗口 (**调试** > **Windows**  >  **进程**)。 如果想要调试 C# 代码，例如，确认是否为适当类型的.NET Framework 配置您的调试器 (例如，托管 (v4\*) 与托管 (v2\*/v3\*) 与托管 (CoreCLR))。

### <a name="-the-current-source-code-is-different-from-the-version-built-into"></a>"… 当前源代码是从...中内置的版本不同"

如果源文件已更改，并且源与正在调试的代码不再匹配，调试器不会设置断点在代码中默认情况下。 通常情况下，此问题发生时更改源文件，但不重新生成的源代码。 若要解决此问题，重新生成项目。 如果生成系统认为该项目已经是最新但没有，可以强制项目系统在重新生成通过再次保存源文件或通过清除项目的生成输出生成前。

在极少数情况下，你可能想要调试而无需匹配的源代码。 调试没有匹配的源代码可以令人混淆的潜在顾客调试体验，因此请确保这是你想要继续操作。

若要禁用这些安全检查，请执行以下操作：
* 若要修改单个断点，请将鼠标悬停在编辑器中的断点图标，然后单击设置 （齿轮） 图标。 查看窗口添加到在编辑器中。 在查看窗口顶部，没有指示的断点的位置的超链接。 单击超链接，以允许修改的断点位置，然后检查**允许源代码与原始不同**。
* 若要修改此设置对所有断点，请转到**调试** > **选项和设置**。 在 **“调试”/“常规”** 页上，清除 **“要求源文件与原始版本完全匹配”** 选项。 请务必重新启用此选项，在完成时调试。

## <a name="the-breakpoint-was-successfully-set-no-warning-but-didnt-hit"></a>断点已成功设置 （无警告），但未命中

本部分提供信息以对问题进行故障排除时调试器未显示任何警告 – 断点是一个实心的红色圆时主动进行调试，但未命中断点。

下面是要检查的几个事项：
1. 如果在多个进程或多台计算机运行你的代码，请确保你正在调试的正确的进程或计算机。
2. 确认你的代码正在运行。 若要测试你的代码运行，将调用添加到`System.Diagnostics.Debugger.Break`(C#/VB) 或`__debugbreak`(C++) 到在您尝试设置了断点，然后重新生成你的项目的代码行。
3. 如果你正在调试优化的代码，请确保在其中设置断点的函数不被内联到另一个函数。 `Debugger.Break`如何工作的上一个检查中所述的测试，测试以及此问题。

## <a name="i-deleted-a-breakpoint-but-i-continue-to-hit-it-when-i-start-debugging-again"></a>我删除了断点，但在再次启动调试时继续命中该断点

如果在调试时删除了断点，可能在下一步启动调试的时再次命中该断点。 要停止命中此断点，请确保从 **“断点”** 窗口删除该断点的所有实例。
