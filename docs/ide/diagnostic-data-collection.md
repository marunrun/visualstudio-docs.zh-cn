---
title: 诊断数据和系统生成的日志
ms.date: 05/24/2018
ms.topic: conceptual
author: jillre
ms.author: michma
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b3f3774a816ca31bfcdd4013d35dadbb1737e5ab
ms.sourcegitcommit: a77158415da04e9bb8b33c332f6cca8f14c08f8c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2020
ms.locfileid: "86387247"
---
# <a name="system-generated-logs-collected-by-visual-studio"></a>由 Visual Studio 收集的系统生成的日志

Visual Studio 收集系统生成的日志以修复问题并通过 [Visual Studio 客户体验改善计划](visual-studio-experience-improvement-program.md)提升产品的质量。 本文介绍我们收集的数据类型以及使用数据的方式。 还为扩展作者提供一些关于如何避免个人信息或敏感信息意外泄露的提示。

## <a name="types-of-collected-data"></a>收集的数据类型

Visual Studio 收集崩溃、UI 无响应以及 CPU 或内存使用率偏高等方面的系统生成的日志。 我们还会收集产品安装或使用期间遇到的错误的相关信息。 收集的数据会基于错误而有所不同，且会包括堆栈跟踪、内存转储和异常信息：

- 对于很高的 CPU 使用率和无响应的情况，会收集相关 Visual Studio 线程的堆栈跟踪信息。

- 如果部分线程的堆栈跟踪信息不足以确定问题的根本原因（例如崩溃、无响应还是内存使用率偏高），我们会收集内存转储。 转储代表出现错误时的进程状态。

- 对于意外的错误情况，例如在尝试向文件或磁盘写入内容时出现的异常，我们会收集该异常的相关信息。 此信息包括异常的名称、出现异常的线程的堆栈跟踪、异常的相关消息以及此特定异常的其他相关信息。

   下面是所收集数据的一个示例，显示了异常名称、堆栈跟踪以及异常消息：

   ```text
   "Reserved.DataModel.Fault.Exception.TypeString": "System.IO.IOException",
   "Reserved.DataModel.Fault.Exception.StackTrace": "System.IO.__Error.WinIOError(Int32,String)\r\n
   System.IO.FileStream.Init(String,FileMode,FileAccess,Int32,Boolean,FileShare,Int32,FileOptions,SECURITY_ATTRIBUTES,String,Boolean,Boolean,Boolean)\r\n
   System.IO.FileStream..ctor(String,FileMode,FileAccess,FileShare,Int32,FileOptions,String,Boolean,Boolean,Boolean)\r\nSystem.IO.StreamWriter.CreateFile(String,Boolean,Boolean)\r\n
   System.IO.StreamWriter..ctor(String,Boolean,Encoding,Int32,Boolean)\r\n
   System.IO.StreamWriter..ctor(String,Boolean)\r\n
   System.IO.File.CreateText(String)\r\n
   Microsoft.VisualStudio.Setup.Services.FileSystem.CreateText(String,Boolean)\r\n
   Microsoft.VisualStudio.Setup.Cache.ChannelManifestRepository.WriteChannelManifest(IChannelManifest,String,String)\r\n
   Microsoft.VisualStudio.Setup.Cache.ChannelManifestRepository.AddChannel(ChannelManifestPair,Boolean)\r\n
   Microsoft.VisualStudio.Setup.Cache.CacheManager.AddChannel(ChannelManifestPair,Boolean)\r\n
   Microsoft.VisualStudio.Setup.ChannelManager.\<UpdateAsync>d__37.MoveNext()\r\n”,
   "Reserved.DataModel.Fault.Exception.Message": " The process cannot access the file 'C:\\Users\\[UserName]\\AppData\\Local\\Microsoft\\VisualStudio\\Packages\\_Channels\\4CB340F5\\channelManifest.json' because it is being used by another process."
   ```

## <a name="how-we-use-system-generated-logs"></a>我们如何使用系统生成的日志

判定错误的根本原因的工作流会各不相同，具体取决于错误的类型和严重性。

### <a name="error-classification"></a>错误分类

基于日志对错误进行了分类和计数，以确定调查的优先顺序。 例如，我们可能会发现，在产品的版本 \<x> 中，“System.IO.FileStream.Init”处的“System.IO.\__Error.WinIOError”出现了 500 次，并且在该版本中的出现率是最高的。

### <a name="work-items-for-tracking"></a>用于跟踪的工作项

为按优先级排列的各个错误创建工作项并分配给工程师以进行调查。 这些工作项通常包含分类、优先级以及与错误类型相关的诊断信息。 此信息派生自收集的系统生成的错误日志。 例如，某次崩溃的工作项可能包含出现崩溃的堆栈跟踪。

### <a name="error-investigation"></a>错误调查

工程师们使用工作项中的可用信息来确定错误的根本原因。 在某些情况下，他们需要比工作项中的内容更多的信息，他们这时候会参考收集到的原始的系统生成的日志。 例如，工程师可能会检查内存转储，以了解产品的崩溃情况。

## <a name="tips-for-extension-authors"></a>对扩展作者的提示

扩展作者应避免在模块、类型和方法名称中使用个人信息或其他敏感信息，从而限制个人信息的公开程度。 如果堆栈上的代码出现崩溃或类似的错误，此信息会被收集为系统生成的日志的一部分。

## <a name="opt-out-of-data-collection"></a>选择退出数据收集

鉴于我们收集数据的目的以及数据访问和保留的相关约束，建议使用 Visual Studio 和 Windows 的默认隐私设置。 不过你可以[选择退出](../ide/visual-studio-experience-improvement-program.md#opt-in-or-out) Visual Studio 体验改善计划。 若要选择退出所有程序的系统生成的日志收集，请参阅 [Windows 10 中的诊断、反馈和隐私](https://privacy.microsoft.com/windows-10-feedback-diagnostics-and-privacy)。 根据使用的 Windows 版本，选项可能有所不同。

## <a name="see-also"></a>请参阅

- [Visual Studio 客户体验改善计划](visual-studio-experience-improvement-program.md)
- [Windows 10 中的诊断、反馈和隐私](https://privacy.microsoft.com/windows-10-feedback-diagnostics-and-privacy)