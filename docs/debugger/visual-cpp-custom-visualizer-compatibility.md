---
title: Visual C /C++自定义可视化工具兼容性
ms.date: 01/28/2019
ms.prod: visual-studio-dev16
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- debugging assertions
- assertions, debugging
- assertions, assertion failures
- Assertion Failed dialog box
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.openlocfilehash: 32e38dd3bba8a1127d8756972b73e8b47a514f1b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62901161"
---
# <a name="visual-cc-custom-visualizer-compatibility"></a>Visual C /C++自定义可视化工具兼容性

在 Visual Studio 2019，视觉对象中启动C++包括用于托管其占用大量内存的组件使用外部的 64 位进程使用改进的调试器。 作为此更新，某些扩展到 Visual C 的一部分 /C++表达式计算器必须更新，以使它们与新的调试器兼容。

如果您当前正在使用旧版 C /C++ EE 外接程序或 C /C++自定义可视化工具，您可以关闭此外部过程的使用情况通过转到**工具** > **选项** > **调试**，再取消选中**加载调试符号在外部进程 （仅限本机） 中**。 如果取消选择此选项，将出现在 IDE (devenv.exe) 进程内的内存使用率显著增加。 因此，如果想要调试大型项目，则建议使用扩展的所有者，以使其与此调试选项兼容。

如果你是旧版 C 的所有者 /C++ EE 外接程序或 C /C++自定义可视化工具，可以找到有关选择加入上加载你的工作进程中的扩展的详细信息[Concord 扩展性示例 wiki](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Worker-Process-Remoting)。 此外可以找到[C /C++自定义可视化工具示例](https://github.com/Microsoft/ConcordExtensibilitySamples/tree/master/CppCustomVisualizer)。