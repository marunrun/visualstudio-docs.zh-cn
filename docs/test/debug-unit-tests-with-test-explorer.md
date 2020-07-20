---
title: 使用测试资源管理器调试单元测试
description: 了解如何在 Visual Studio 中使用测试资源管理器调试单元测试。
ms.date: 07/14/2020
ms.topic: how-to
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2def56c6a3860ce0476f448f87bdde25c7970807
ms.sourcegitcommit: a77158415da04e9bb8b33c332f6cca8f14c08f8c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2020
ms.locfileid: "86393537"
---
# <a name="debug-and-analyze-unit-tests-with-test-explorer"></a>使用测试资源管理器调试和分析单元测试

可以使用测试资源管理器为你的测试启动调试会话。 使用 Visual Studio 调试程序无缝地逐句通过代码将使你在单元测试和所测试项目之间来回反复。 若要开始调试：

1. 在 Visual Studio 编辑器中，在想要调试的一个或多个测试方法中设置断点。

    > [!NOTE]
    > 因为测试方法可以按任何顺序运行，请在你想要调试的所有测试方法中设置断点。

::: moniker range="vs-2017"
2. 在“测试资源管理器”中，选择测试方法、右键单击选中的方法，然后选择“调试选定测试”。
::: moniker-end
::: moniker range=">=vs-2019"
2. 在“测试资源管理器”中，选择测试方法、右键单击选中的方法，然后选择“调试”。

   ![测试执行详细信息](../test/media/vs-2019/test-explorer-debug.png)
::: moniker-end

   有关该调试程序的详细信息，请参阅[在 Visual Studio 中进行调试](../debugger/debugger-feature-tour.md)。

## <a name="diagnose-test-method-performance-issues"></a>诊断测试方法性能问题

::: moniker range="vs-2017"
若要诊断测试方法为何花费过多时间，请在测试资源管理器中依次选择方法和右键单击菜单中的“配置文件选定测试”。 请参阅[检测分析报告](../profiling/understanding-instrumentation-data-values.md?view=vs-2017)。
::: moniker-end

::: moniker range=">=vs-2019"
若要诊断测试方法为何花费过多时间，请在测试资源管理器中依次选择方法和右键单击菜单中的“配置文件”。 请参阅[检测分析报告](../profiling/understanding-instrumentation-data-values.md?view=vs-2017)。
::: moniker-end

> [!NOTE]
> .NET Core 目前不支持此功能。

## <a name="see-also"></a>请参阅

- [单元测试代码](../test/unit-test-your-code.md)
- [使用测试资源管理器运行单元测试](../test/run-unit-tests-with-test-explorer.md)
- [测试资源管理器常见问题解答](test-explorer-faq.md)
