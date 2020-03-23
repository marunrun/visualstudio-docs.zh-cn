---
title: 启用&禁用托管代码的完整解决方案分析
ms.date: 03/23/2018
ms.topic: conceptual
helpviewer_keywords:
- full solution analysis
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: d699dd74315cfc36820c1cdb4120543e0290b1a1
ms.sourcegitcommit: b32fbbcbc43910b0ed7ce79aa9a22f2ed36ab57e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428187"
---
# <a name="how-to-enable-and-disable-full-solution-analysis-for-managed-code"></a>如何：为托管代码启用和禁用完整的解决方案分析

*完整的解决方案分析*意味着代码分析会检查解决方案中的所有 C# 或 Visual Basic 文件，无论这些文件是否在编辑器中打开。 默认情况下，为 Visual Basic*启用*了完整的解决方案分析，并且*禁用*了 C#。

查看所有文件中的所有问题都很有用，但也可能会分散注意力。 如果解决方案非常大或有许多文件，它会减慢 Visual Studio 的速度。 要限制显示的问题数量并提高 Visual Studio 的性能，可以禁用完整的解决方案分析。 如有必要，可以轻松地重新启用此功能。

在下图中，启用了完整的解决方案分析。 将显示解决方案中的所有文件中的编译器和代码分析问题，即使它们未打开也是如此。

![已启用完整的解决方案分析。](../code-quality/media/fsa_enabled.png)

下图显示了禁用完整解决方案分析后同一解决方案的结果。 在"错误列表"中，只有打开的解决方案文件中的编译器错误和代码分析问题才会显示。

![禁用了完整的解决方案分析。](../code-quality/media/fsa_disabled.png)

## <a name="toggle-full-solution-analysis"></a>切换完整解决方案分析

1. 要打开"**选项"** 对话框，在可视化工作室的菜单栏上选择 **"工具** > **选项**"。

1. 在"**选项**"对话框中，**选择文本编辑器** > **C#** 或**基本** > **高级**。

1. 选择"**启用完整解决方案分析**"复选框以启用完整的解决方案分析，或清除该框以禁用该框。 完成后选择 **"确定**"。

   ![启用完整的解决方案分析复选框。](../code-quality/media/options-enable-full-solution-analysis.png)

## <a name="automatically-disable-full-solution-analysis"></a>自动禁用完整的解决方案分析

如果 Visual Studio 检测到其可以使用 200 MB 或更少的系统内存，则如果启用了完整解决方案分析（以及某些其他功能），它将自动禁用它。 如果发生这种情况，将显示一个警报，通知您 Visual Studio 已禁用某些功能。 通过按钮，您可以重新启用完整的解决方案分析（如果需要）。

![警报文本暂停完整的解决方案分析](../code-quality/media/fsa_alert.png)
