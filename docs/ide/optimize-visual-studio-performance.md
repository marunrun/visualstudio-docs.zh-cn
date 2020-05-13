---
title: 在 Visual Studio 速度较慢的情况下提高性能
titleSuffix: ''
ms.date: 04/11/2018
ms.topic: conceptual
helpviewer_keywords:
- performance [Visual Studio]
author: TerryGLee
ms.author: tglee
manager: jillfra
f1_keywords:
- vs.performancecenter
ms.workload:
- multiple
ms.openlocfilehash: 6495e8506e12c0c5e5f878a23c609fe53a401bde
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75596991"
---
# <a name="optimize-visual-studio-performance"></a>优化 Visual Studio 性能

如果发现 Visual Studio 运行速度缓慢，本文提供了一些建议。 有关如何提高性能的更多建议，还可以查看 [Visual Studio 性能提示和技巧](../ide/visual-studio-performance-tips-and-tricks.md)。

## <a name="upgrade-visual-studio"></a>升级 Visual Studio

如果当前使用 Visual Studio 2015，请免费下载 [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) 或 [Visual Studio 2019](https://visualstudio.microsoft.com/downloads)，以检查其改进性能。 在 Visual Studio 2015 中，解决方案的加载速度要快两到三倍，其他方面的性能也有所改善。 Visual Studio 2017 和 Visual Studio 2019 与 Visual Studio 2015 并行兼容，因此不会因为尝试而丢失任何内容。

::: moniker range="vs-2017"

如果已在使用 Visual Studio 2017，请确保运行版本 15.6 或更高版本。 数据显示，在版本 15.6 中，解决方案的加载速度最高可提升两到三倍。 在[此处](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)下载。

::: moniker-end

## <a name="extensions-and-tool-windows"></a>扩展和工具窗口

安装的扩展可能会使 Visual Studio 速度变慢。 有关管理扩展以提高性能的帮助，请参阅[更改扩展设置以提高性能](../ide/optimize-visual-studio-startup-time.md#extensions)。

同样，工具窗口也可能会使 Visual Studio 速度变慢。 有关管理工具窗口的帮助，请参阅[更改工具窗口设置以提高性能](../ide/optimize-visual-studio-startup-time.md#tool-windows)。

## <a name="hardware"></a>硬件

如果考虑升级硬件，固态硬盘 (SSD) 对性能的影响比额外的 RAM 或更快的 CPU 更大。

若要添加 SSD，为了获得最佳性能，应将 Windows 安装在 SSD 上，而非硬盘驱动器 (HDD)。 Visual Studio 解决方案的驱动器位置似乎没有那么重要。

此外，不要从 USB 驱动器运行解决方案。 请将其复制到 HDD 或 SSD。

## <a name="help-us-improve"></a>帮助我们改进

你的反馈有助于我们改进。 使用“报告问题”功能来“记录”跟踪并发送给我们  。 选择“快速启动”旁边的反馈图标，或从菜单栏中选择“帮助” **“发送反馈”** “报告问题”   >    >   。 有关详细信息，请参阅[如何报告 Visual Studio 的问题](../ide/how-to-report-a-problem-with-visual-studio.md)。

## <a name="see-also"></a>另请参阅

- [性能提示和技巧](../ide/visual-studio-performance-tips-and-tricks.md)
- [Visual Studio blog - Load solutions faster with Visual Studio 2017 version 15.6](https://devblogs.microsoft.com/visualstudio/load-solutions-faster-with-visual-studio-2017-version-15-6/)（Visual Studio 博客 - 使用 Visual Studio 2017 版本 15.6 更快地加载解决方案）
