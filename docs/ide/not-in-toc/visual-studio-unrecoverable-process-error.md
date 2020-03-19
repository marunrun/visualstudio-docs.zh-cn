---
title: 进程遇到不可恢复的错误
ms.date: 06/22/2018
ms.topic: troubleshooting
helpviewer_keywords:
- unrecoverable error
- error, process
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 206fcddca51f8e770e013ff67de6ae3d5562f633
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75585790"
---
# <a name="visual-studio-unrecoverable-process-error"></a>Visual Studio 无法恢复的处理器错误

Visual Studio 使用多个进程外的进程来运行必需的后台任务，如实时单元测试、代码分析器等。 在进程外运行这些进程可提供 Visual Studio 性能优势，例如运行长且资源密集的作业时，Visual Studio 可更快响应。 此外，由于 Visual Studio 是一个 32 位进程，在进程外运行进程可为内存密集型作业提供更大的操作内存空间。

如果 ServiceHub.RoslynCodeAnalysisService.exe 或 ServiceHub.RoslynCodeAnalysisService32.exe 进程出于某种原因结束，弹出信息栏会显示以下消息   ：

“很抱歉，Visual Studio 使用的进程遇到不可恢复的错误。  建议保存你的工作，然后关闭并重新启动 Visual Studio。”

如果看到此消息，应保存工作，然后关闭并重新启动 Visual Studio。

## <a name="list-of-processes"></a>进程列表

下面是 Visual Studio 使用的进程外的进程列表。 此列表包括在特定工作流或方案中启动的进程，因此在大多数情况下，它们并非全部同时运行。

- Microsoft.Alm.Shared.Remoting.RemoteContainer.dll
- Microsoft.CodeAnalysis.LiveUnitTesting.EntryPoint
- PerfWatson2.exe
- ServiceHub.Host.Node.x86.exe
- ServiceHub.IdentityHost.exe
- ServiceHub.VSDetouredHost.exe
- ServiceHub.SettingsHost.exe
- ServiceHub.Host.CLR.x86.exe
- ServiceHub.RoslynCodeAnalysisService32.exe
- ServiceHub.RoslynCodeAnalysisService.exe
- WindowsAzureGuestAgent.exe
- WindowsAzureTelemetryService.exe
- WaAppAgent.exe

如果其中某个进程意外终止，Visual Studio 中的某些功能将停止工作。 对于某些进程，失去功能可能没有重大影响。 对于其他进程，会影响 Visual Studio 的稳定性并显示错误消息。
