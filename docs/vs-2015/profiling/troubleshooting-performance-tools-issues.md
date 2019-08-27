---
title: 性能工具问题疑难解答 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: troubleshooting
ms.assetid: 0b61cdf7-75b7-4abd-aff2-7bd997717626
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 575f17c641eb057dc01fb3302098bd9f8b47f9c5
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63431616"
---
# <a name="troubleshooting-performance-tools-issues"></a>性能工具问题疑难解答
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用分析工具时，可能会遇到以下问题之一：  
  
- [分析工具未收集任何数据](#NoDataCollected)  
  
- [性能视图和报告显示函数名的编号](#NoSymbols)  
  
## <a name="NoDataCollected"></a> 分析工具未收集任何数据  
 分析应用程序之后，未创建分析数据 (.vsp) 文件，你在“输出”窗口或命令窗口中收到以下警告：  
  
 PRF0025：未收集到任何数据。  
  
 此问题可能由多个问题导致：  
  
- 使用采样或 .NET 内存方法分析的进程启动的子进程成为执行应用程序工作的进程。 例如，某些应用程序读取命令行以确定它们是作为 Windows 应用程序还是命令行应用程序启动。 如果请求了 Windows 应用程序，则原始进程会启动一个配置为 Windows 应用程序的新进程，然后原始进程退出。 因为分析工具不会自动收集子进程的数据，所以不会收集任何数据。  
  
     若要在这种情况下收集分析数据，请将探查器附加到子进程而不是使用探查器启动应用程序。 有关详细信息，请参阅[如何：附加和分离性能工具正在运行的进程](../profiling/how-to-attach-and-detach-performance-tools-to-running-processes.md)和[附加 (VSPerfCmd)](../profiling/attach.md)  
  
## <a name="NoSymbols"></a> 性能视图和报告显示函数名的编号  
 分析应用程序之后，在报告和视图中看到编号而不是函数名。  
  
 导致此问题的原因是分析工具分析引擎无法找到 .pdb 文件，这些文件包含将源代码信息（如函数名和行号）映射到已编译的文件的符号信息。 默认情况下，编译器会在生成应用程序文件时创建 .pdb 文件。 对 .pdb 文件的本地目录的引用存储在编译的应用程序中。 分析引擎会在引用的目录中查找 .pdb 文件的，然后在当前包含应用程序文件的文件中查找。 如果未找到 .pdb 文件，则分析引擎使用函数偏移量而不是函数名。  
  
 可以通过两种方式之一来修复此问题：  
  
- 找到 .pdb 文件并将它们放置在应用程序文件所在的目录中。  
  
- 在分析数据 (.vsp) 文件中嵌入符号信息。 有关详细信息，请参阅[使用性能数据文件保存符号信息](../profiling/saving-symbol-information-with-performance-data-files.md)。  
  
> [!NOTE]
> 分析引擎要求 .pdb 文件的版本与编译的应用程序文件相同。 来自应用程序文件的早期版本或更高版本的 .pdb 文件无法正常工作。
