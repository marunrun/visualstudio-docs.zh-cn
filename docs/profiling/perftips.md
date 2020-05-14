---
title: 性能提示 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 509d2d4f-48a5-4cdf-acad-6f7b75421303
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 93703bdd4bf2f0046176ceb1f6febd5564f61705
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "71128309"
---
# <a name="perftips"></a>性能提示
Visual Studio 调试器 *性能提示* 和调试器集成的 **“诊断工具”** 可帮助在调试时监视和分析应用的性能。

 虽然调试器集成的诊断工具是在开发时注意性能问题的极佳方式，但是调试器可能会显著影响应用的性能。 若要收集更准确的性能数据，请考虑使用也在调试器外部作为性能调查的其他部分运行的 Visual Studio 诊断工具。 请参阅[运行带/不带调试程序的分析工具](../profiling/running-profiling-tools-with-or-without-the-debugger.md)。

## <a name="perftips"></a>性能提示
 调试器在断点或单步执行操作中停止执行时，中断与上一个断点之间经过的时间会显示为在编辑器窗口中的提示。 有关详细信息，请参阅 [PerfTips：使用 Visual Studio 调试时快速查看性能信息](https://devblogs.microsoft.com/devops/perftips-performance-information-at-a-glance-while-debugging-with-visual-studio/)。

 ![PerfTip](../profiling/media/dbgdiag_perf_perftip.png "DBGDIAG_PERF_PerfTip")

## <a name="diagnostics-tools-window"></a>“诊断工具”窗口
 断点以及关联计时数据记录在“诊断工具”窗口中  。

 下图显示 Visual Studio 2015 Update 1 中的“诊断工具”  窗口：

 ![DiagnosticTools&#45;Update1](../profiling/media/diagnostictools-update1.png "DiagnosticTools-Update1")

- **“中断事件”** 时间线会标记在调试会话中命中的断点。 在 **“调试器”** 详细信息列表中单击事件以选择它。

- **“CPU 使用率”** 关系图会显示调试会话中所有处理器核心间的 CPU 使用情况变化。

- **“调试器”** 详细信息窗格的 **“事件”** 列表包含用于每个中断事件的项。

- 中断事件的 **“持续时间”** 列显示事件与上一个断点之间经过的时间。

## <a name="turn-perftips-on-or-off"></a>打开或关闭性能提示
 启用或禁用性能提示：

1. 在 **“调试”** 菜单上，选择 **“选项”** 。

2. 选中或清除 **“在调试过程中显示占用时间性能提示”** 。

## <a name="turn-the-diagnostic-tools-window-on-or-off"></a>打开或关闭“诊断工具”窗口
 启用或禁用“诊断工具”窗口：

1. 在 **“调试”** 菜单上，选择 **“选项”** 。

2. 选中或清除 **“在调试过程中启用诊断工具”** 。

## <a name="see-also"></a>请参阅
- [使用 Visual Studio 分析](../profiling/index.yml)
- [首先了解分析工具](../profiling/profiling-feature-tour.md)
