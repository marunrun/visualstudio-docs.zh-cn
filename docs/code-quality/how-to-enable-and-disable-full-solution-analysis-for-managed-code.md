---
title: 启用和禁用托管代码的完整解决方案分析
ms.date: 03/23/2018
ms.topic: conceptual
helpviewer_keywords:
- full solution analysis
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: a445439014e3b1f68b634865265089eb68e790a6
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/28/2019
ms.locfileid: "66260879"
---
# <a name="how-to-enable-and-disable-full-solution-analysis-for-managed-code"></a>如何：启用和禁用托管代码的完整解决方案分析

*完整解决方案分析*是 Visual Studio 功能，使您可以查看仅在打开视觉对象中的代码分析问题C#或 Visual Basic 文件在解决方案中，还是也在已关闭的代码文件中。 默认情况下是完整解决方案分析*启用*对于 Visual Basic，并*禁用*视觉对象C#。

可能会很有用，若要查看所有文件中的所有问题，但它也可以让人分散注意力。 如果你的解决方案非常大或包含多个文件，其速度 Visual Studio 变慢。 若要限制显示的问题数并改进 Visual Studio 性能，可以禁用完整解决方案分析。 如有必要，可以轻松地重新启用此功能。

## <a name="to-toggle-full-solution-analysis"></a>若要切换完整解决方案分析

1. 若要打开**选项**对话框中，在 Visual Studio 的菜单栏上选择**工具** > **选项**。

1. 在中**选项**对话框框中，选择**文本编辑器** >  **C#** 或**基本** >  **高级**。

1. 选择**启用完整解决方案分析**复选框以启用完整解决方案分析或清除相应的框以禁用它。 选择**确定**完成后。

    ![启用完整解决方案分析复选框。](../code-quality/media/options-enable-full-solution-analysis.png)

## <a name="results-of-enabling-and-disabling-full-solution-analysis"></a>启用和禁用完整解决方案分析的结果

在以下屏幕截图中，您可以看到结果时启用完整解决方案分析。 所有错误和中的代码分析问题*所有*的解决方案中的文件显示，而不考虑文件是否都打开。

![启用完整解决方案分析。](../code-quality/media/fsa_enabled.png)

禁用完整解决方案分析之后，下面的屏幕截图显示同一解决方案中的结果。 仅错误和打开解决方案文件中的代码分析问题显示在**错误列表**。

![禁用完整解决方案分析。](../code-quality/media/fsa_disabled.png)

## <a name="automatically-disable-full-solution-analysis"></a>会自动禁用完整解决方案分析

如果 Visual Studio 检测到的 200 MB 或更少的系统内存可供它，它会自动禁用完整解决方案分析 （和其他一些功能） 如果已启用。 如果发生这种情况，会显示警报，通知你 Visual Studio 已禁用某些功能。 按钮可以重新启用完整解决方案分析，如果你想。

![警报文本中挂起完整解决方案分析](../code-quality/media/fsa_alert.png)