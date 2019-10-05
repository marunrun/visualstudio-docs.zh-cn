---
title: 启用 & 禁用托管代码的完整解决方案分析
ms.date: 03/23/2018
ms.topic: conceptual
helpviewer_keywords:
- full solution analysis
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 0b192b29190d530d22943e8ba2a396ae1fe9ad87
ms.sourcegitcommit: 39a04f42d23597b70053686d7e927ba78f38a9a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2019
ms.locfileid: "71975129"
---
# <a name="how-to-enable-and-disable-full-solution-analysis-for-managed-code"></a>如何：启用和禁用托管代码的完整解决方案分析

*完整的解决方案分析*意味着代码分析检查解决方案中C#的所有或 Visual Basic 文件，无论它们是否在编辑器中打开。 默认情况下，将为 Visual Basic*启用*完整解决方案分析 ，并C#为禁用。

这对于查看所有文件中的所有问题很有用，但也可能会分散注意力。 如果你的解决方案非常大或包含多个文件，则会降低 Visual Studio 的运行速度。 若要限制显示的问题数并改善 Visual Studio 性能，可以禁用完整解决方案分析。 必要时，可以轻松地重新启用此功能。

在下图中，启用了完整解决方案分析。 将显示解决方案中所有文件的编译器和代码分析问题，即使它们未打开也是如此。

![已启用完整解决方案分析。](../code-quality/media/fsa_enabled.png)

下图显示了禁用完整解决方案分析后相同解决方案的结果。 只有打开的解决方案文件中的编译器错误和代码分析问题才会出现在错误列表中。

![已禁用完整解决方案分析。](../code-quality/media/fsa_disabled.png)

## <a name="toggle-full-solution-analysis"></a>切换完整解决方案分析

1. 若要打开 "**选项**" 对话框，请在 Visual Studio 的菜单栏中选择 "**工具**"  > **选项**。

1. 在 "**选项**" 对话框中，选择 "**文本编辑器**@no__t**C#** -2" 或 "**基本** > **高级**"。

1. 选中 "**启用完整解决方案分析**" 复选框以启用完整解决方案分析，或者清除该复选框以禁用它。 完成后，请选择 **"确定"** 。

   ![启用完整解决方案分析复选框。](../code-quality/media/options-enable-full-solution-analysis.png)

## <a name="automatically-disable-full-solution-analysis"></a>自动禁用完整解决方案分析

如果 Visual Studio 检测到可用于 200 MB 或更少的系统内存，则它会自动禁用完整解决方案分析（以及其他一些功能）（如果已启用）。 如果出现这种情况，则会出现一个警报，通知你 Visual Studio 已禁用某些功能。 利用按钮，可以根据需要重新启用完整解决方案分析。

![警报文本中挂起完整解决方案分析](../code-quality/media/fsa_alert.png)