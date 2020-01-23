---
title: 如何提高解决性能问题的几率
description: 有关在 Visual Studio 中提交性能问题的其他信息和最佳实践
author: seaniyer
ms.author: seiyer
ms.date: 11/19/2019
ms.topic: reference
ms.openlocfilehash: 119de27298acafee7dc563a30246b18da42f9f29
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/13/2020
ms.locfileid: "75918166"
---
# <a name="how-to-increase-the-chances-of-a-performance-issue-being-fixed"></a>如何提高解决性能问题的几率

Visual Studio 用户常使用[报告问题](/visualstudio/ide/how-to-report-a-problem-with-visual-studio?view=vs-2019)工具来报告一系列问题。 Visual Studio 团队在用户反馈中发现故障和运行缓慢的趋势，并解决影响大量用户的问题。 特定反馈工单的可操作性越高，产品团队就越有可能快速诊断和解决问题。 本文档介绍了在报告故障或运行缓慢问题时可用于提高这些问题的可操作性的最佳做法。

## <a name="general-best-practices"></a>一般最佳实践

Visual Studio 是一个大型的综合平台，支持多种语言、项目类型和平台等等。 它的性能取决于会话中安装和启用的组件、安装的扩展、Visual Studio 设置、计算机配置，以及正在编辑的代码的形状。 考虑到变量数目，即使看到的症状相同，也很难判断某个用户的问题报告是否与其他用户的问题报告一样具有相同的基础问题。 鉴于这种情况，下面介绍了一些最佳做法，可确保提高诊断出特定问题报告的可能性。

**尽量提供具体的标题**

查找所报告问题的不同签名，并尽可能多地包含在标题中。 如果是描述性标题，具有无关问题（但表面症状相同）的用户就不太可能对你的工单进行投票或评论，因此会加大问题的诊断难度  。

**如果存在疑问，请记录新的问题报告**

许多问题可能没有任何特殊签名或重现步骤。 在这种情况下，新报告要比投票支持和评论报告了类似表面症状的其他报告更好  。 根据报告类型，如本文档后面所述，将其他诊断文件加入到报告中。

**针对具体问题的最佳做法**

下面介绍了在没有合适诊断文件的情况下难以诊断的问题。 在确定了与你的问题最相符的情况之后，请按照针对这种情况的反馈步骤进行操作。

-   [故障：](#crashes)进程 (Visual Studio) 意外终止时发生故障。

-   [无响应：](#unresponsiveness)VS 长时间处于无响应状态。

-   [运行缓慢问题：](#slowness-and-high-cpu-issues)VS 中的任何特定操作都比预期慢

-   [CPU 使用率过高：](#slowness-and-high-cpu-issues)CPU 使用率长时间高乎寻常

-   [进程外问题：](#out-of-process-issues)Visual Studio 附属进程导致的问题

## <a name="crashes"></a>故障
进程 (Visual Studio) 意外终止时发生故障。

**可直接重现的故障**

可直接重现的故障具有以下所有特征：

- 可以按照一组已知步骤观察到

- 可以在多台计算机上（如有）观察到

- 可以在能够通过链接访问或在反馈中提供的示例代码或项目中重现（如果步骤涉及打开项目或文档）

对于这类问题，请按照“[如何报告问题](/visualstudio/ide/how-to-report-a-problem-with-visual-studio-2017)”中的步骤进行操作，并确保包含：

-   问题重现步骤

-   上述独立重现项目。 如果无法独立重现，请包含：

    -   打开的项目的语言（C\#、C++ 等）

    -   项目类型（控制台应用程序、ASP.NET 等）


> [!NOTE]
> **最有价值的反馈：** 对于这种情况，最有价值的反馈是一组问题重现步骤和示例源代码。

**未知故障**

如果不确定导致故障的原因或它们像是随机发生的，则可在 Visual Studio 每次发生故障时在本地捕获转储并将其附加到单独的反馈项。 若要在 Visual Studio 发生故障时本地保存转储，请在管理员命令窗口中运行以下命令：

```
reg add "HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Windows\\Windows Error
Reporting\\LocalDumps\\devenv.exe"

reg add "HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Windows\\Windows Error
Reporting\\LocalDumps\\devenv.exe" /v DumpType /t REG_DWORD /d 2

reg add "HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Windows\\Windows Error
Reporting\\LocalDumps\\devenv.exe" /v DumpCount /t REG_DWORD /d 2

reg add "HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Windows\\Windows Error
Reporting\\LocalDumps\\devenv.exe" /v DumpFolder /t REG_SZ /d "C:\\CrashDumps"
```

根据需要自定义转储计数和转储文件夹。 有关这些设置的详细信息，请单击[此处](/windows/win32/wer/collecting-user-mode-dumps)。

> [!NOTE]
> 使用任务管理器捕获的转储可能位数不正确，因此用处不大。 上述过程是捕获堆转储的首选方法。 如果想使用任务管理器，请关闭当前正在运行的命令，启动 32 位任务管理器 (%windir%\\syswow64\\taskmgr.exe) 并通过它收集堆转储。

> [!NOTE] 
> 该方法生成的每个转储文件的大小上限为 4 GB。 请确保将 DumpFolder 设置到具有足够驱动器空间的位置，或适当调整 DumpCount。

每当 Visual Studio 发生故障时，它都会在配置的位置创建一个转储文件（devenv.exe.[number].dmp 文件）  。

然后，使用 Visual Studio 的“报告问题…”功能。 利用该功能，可以附加相应的转储。

1.  找到当前报告的故障的转储文件（查找具有正确创建时间的文件）

2.  如果可能，请在提交反馈之前压缩文件 (\*.zip) 以减小其大小

3.  按照[如何报告问题](/visualstudio/ide/how-to-report-a-problem-with-visual-studio-2017)中的步骤操作，并将堆转储附加到新的反馈项。

> [!NOTE] 
> **最有价值的反馈：** 对于这种情况，最有价值的反馈是发生故障时捕获的堆转储。

## <a name="unresponsiveness"></a>无响应
VS 长时间处于无响应状态。

**可直接重现的无响应**

正如在有关故障的相应部分中所述，对于那些能轻松重现的、可在多台计算机上观察到的以及能够在小型示例中演示的问题，最有价值的反馈报告应该包含问题重现步骤以及用于演示问题的示例源代码。

**未知的无响应**

如果无响应状态以一种不可预知的方式出现，请在下一次发生时启动 Visual Studio 的新实例并从该实例报告问题。
在[“记录”屏幕](/visualstudio/ide/how-to-report-a-problem-with-visual-studio?view=vs-2019#record-a-repro)中，确保选择无响应的 Visual Studio 会话。

如果无响应的 Visual Studio 实例是在管理员模式下启动的，那么第二个实例也需要在管理员模式下启动。

>[!NOTE] 
> **最有价值的反馈：** 对于这种情况，最有价值的反馈是在无响应时捕获的堆转储。

## <a name="slowness-and-high-cpu-issues"></a>运行缓慢和 CPU 使用率过高问题

在运行缓慢的操作或 CPU 使用率过高的事件正在进行时捕获的性能跟踪能最大限度提高运行缓慢和 CPU 使用率过高问题的可操作性。

>[!NOTE] 
> 如果可能，请在单独的特定反馈报告中分别描述每种情况。
例如，如果键入操作和导航都很缓慢，请对每个问题执行一次下面的步骤。 这样有助于产品团队分别找出特定问题的原因。

为了在捕获性能时获得最佳结果，请执行以下步骤：

1.  如果尚未运行，请打开 Visual Studio 的副本，在其中重现相关问题

    -   设置好所有内容，以重现该问题。 例如，如果需要加载特定的项目并打开特定文件，请确保完成这两个步骤后再继续操作。

    -   如果未报告特定于加载解决方案的问题，打开解决方案后尝试等待 5-10 分钟（或更长时间，具体取决于解决方案大小），然后再记录性能跟踪  。 解决方案加载过程会生成大量数据，因此等待几分钟可帮助我们专注于处理当前报告的特定问题。

2.  启动 Visual Studio 的第二个副本，但不打开解决方案 

3.  在 Visual Studio 的新副本中，打开“报告问题”工具 

4.  按照[如何报告问题](/visualstudio/ide/how-to-report-a-problem-with-visual-studio-2017)中的步骤操作，直到完成“提供跟踪和堆转储（可选）”步骤。

5.  选择记录 Visual Studio 的第一个副本（即遇到性能问题的副本）并开始记录。

    -   步骤记录器应用程序随即显示并开始记录。

    -   在记录过程中，在 Visual Studio 的第一个副本中执行有问题的操作  。 如果在记录的时间内未出现特定的性能问题，则很难将其解决。

    -   如果操作短于 30 秒并且可以轻松重现，请重现该操作以进一步演示问题。

    -   大多数情况下，60 秒的跟踪足以演示问题，尤其是在有问题的操作持续（或重复） 30 秒以上时。 可以根据需要调整持续时间，以捕获要修复的行为。

6.  对于运行缓慢的操作或 CPU 使用率过高的事件，当它们完成后，立即在步骤记录器中单击“停止记录”。 处理性能跟踪可能需要几分钟时间。

7.  完成后，需要在反馈中添加多个附件。 附加可帮助重现问题的其他文件（示例项目、屏幕截图、视频等）。

8.  提交反馈。

记录性能跟踪时，如果要报告的运行缓慢的操作或 CPU 使用率过高的事件结束，则立即停止记录。 如果收集的信息过多，最早的信息将被覆盖。 如果在感兴趣的操作之后没有很快（几秒钟内）停止跟踪，有用的跟踪数据将被覆盖。

请勿直接将性能跟踪附加到开发者社区网站中的现有反馈项。 请求/提供附加信息是 Visual Studio 内置“报告问题”工具中受支持的工作流。 如果需要进行性能跟踪才能解析以前的反馈项，我们会将反馈项的状态设置为“需要更多信息”，然后可以用报告新问题的方式对其进行回应。 有关详细说明，请参阅“报告问题”工具文档中的[“需要更多信息”部分](/visualstudio/ide/how-to-report-a-problem-with-visual-studio-2017?view=vs-2017#when-further-information-is-needed-need-more-info)。

> [!NOTE] 
> **最有价值的反馈：** 几乎对于所有运行缓慢/CPU 使用率过高的问题来说，最有价值的反馈都概括说明了你已尝试的操作，以及在该时间段内捕获行为的性能跟踪 (\*.etl.zip)。

**高级性能跟踪**

“报告问题”工具中的跟踪收集功能就足以应对大多数情况。 但有时需要加强控制跟踪集合（例如，缓冲区更大的跟踪），此时适合使用 PerfView 工具。 使用 PerfView 工具手动记录性能跟踪的步骤可在 [Recording performance traces with PerfView](https://github.com/dotnet/roslyn/wiki/Recording-performance-traces-with-PerfView)（使用 PerfView 记录性能跟踪）页中找到。

## <a name="out-of-process-issues"></a>进程外问题

> [!NOTE]
> 从 Visual Studio 2019 版本 16.3 开始，进程外日志会自动附加到使用“报告问题”工具提交的反馈。 但是，如果问题可直接重现，遵循以下步骤仍然可以帮助添加附加信息，以帮助更好地诊断问题。

有许多与 Visual Studio 并行运行的附属进程，并从 Visual Studio 主进程外提供各种功能。 如果其中一个附属进程发生错误，则通常在 Visual Studio 端看到“StreamJsonRpc. RemoteInvocationException”或“StreamJsonRpc ConnectionLostException”。

最能使这些类型的问题付诸实践的是提供可通过以下步骤收集的其他日志：

1.  如果这是直接可重现的问题，请从删除 %temp%/servicehub/logs  文件夹开始。 如果无法重现此问题，请保持此文件夹不变，并忽略以下项目符号：

    -   将全局环境变量 ServiceHubTraceLevel  设置为“全部” 
    -   重现此问题。

2.  在[此处](https://www.microsoft.com/download/details.aspx?id=12493)下载 Microsoft Visual Studio 和 .NET Framework 日志收集工具。
3.  运行该工具。 这会将一个 zip 文件输出到 %temp%/vslogs.zip  。 请将该文件附加到你的反馈。

## <a name="see-also"></a>请参阅

* [Visual Studio 反馈选项](../ide/feedback-options.md)
* [报告 Visual Studio for Mac 的问题](/visualstudio/mac/report-a-problem)
* [报告 C++ 问题](/cpp/how-to-report-a-problem-with-the-visual-cpp-toolset)
* [Visual Studio 开发者社区](https://developercommunity.visualstudio.com/)
* [开发人员社区数据隐私](developer-community-privacy.md)
