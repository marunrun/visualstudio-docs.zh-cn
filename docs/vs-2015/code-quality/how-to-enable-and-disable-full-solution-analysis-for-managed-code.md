---
title: 如何：启用和禁用托管代码的完整解决方案分析 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
helpviewer_keywords:
- full solution analysis
ms.assetid: 04315147-5792-47f0-8b5f-9ac8413c6a57
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 72b27bf9dcc1f0ee8a222ac701f2ffae4fc68614
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72646283"
---
# <a name="how-to-enable-and-disable-full-solution-analysis-for-managed-code"></a>如何：启用和禁用托管代码的完整解决方案分析
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

备注
> 本主题仅适用于 Visual Studio 2015 Update 3 RC 和更高版本。

 *完整的解决方案分析*是一项 Visual Studio 功能，使你能够选择是仅在解决方案中打开的视觉C#对象或 Visual Basic 文件中看到代码分析问题，还是 Visual Basic 在C#你的解决方案.

 尽管能够查看所有文件中的所有问题都很有用，但如果您的解决方案非常大或有大量文件，则可能会对 Visual Studio 进行分散甚至缓慢的影响。  若要限制显示的问题数并改善 Visual Studio 性能，可以禁用完整解决方案分析。 如果需要，可以轻松地重新启用此功能。

#### <a name="to-toggle-full-solution-analysis"></a>切换完整解决方案分析

1. 在 Visual Studio 中的主菜单上，选择 "**工具** &#124; " "**选项**" 以查看 "**选项**" 对话框。

2. 在 "**选项**" 对话框中，选择 "**文本编辑器** &#124; **C#** " 或 "**基本** &#124; **高级**"。

3. 选中 "**启用完整解决方案分析**" 复选框以启用完整解决方案分析，或者清除该复选框以禁用它。 完成后，选择 **"确定"** 按钮。

     ![启用完整解决方案分析复选框。](../code-quality/media/fsa-toolsoptions.png "FSA_ToolsOptions")

## <a name="results-of-enabling-and-disabling-full-solution-analysis"></a>启用和禁用完整解决方案分析的结果
 在下面的屏幕截图中，可以看到启用了完整解决方案分析后的结果。 解决方案中的*所有*文件中的所有错误和代码分析问题都将出现，无论这些文件是否已打开。

 ![已启用完整解决方案分析。](../code-quality/media/fsa-enabled.png "FSA_Enabled")

 下面的屏幕截图显示了禁用完整解决方案分析后相同解决方案的结果。 只有打开的解决方案文件中的错误和代码分析问题才会出现在错误列表中。

 ![已禁用完整解决方案分析。](../code-quality/media/fsa-disabled.png "FSA_Disabled")

## <a name="automatically-disabling-full-solution-analysis"></a>自动禁用完整解决方案分析
 如果 Visual Studio 检测到200MB 或更少的系统内存可用，则会自动禁用完整解决方案分析（以及其他一些功能）（如果已启用）。 如果出现这种情况，则会出现警报，告知你这一点。 如果要执行此操作，可以使用按钮重新启用完整解决方案分析。

 ![暂停完整解决方案分析的警报文本](../code-quality/media/fsa-alert.png "FSA_Alert")

## <a name="additional-details"></a>其他详细信息
 默认情况下，将对 Visual Basic 启用完整解决方案分析，并对C#视觉对象禁用完整解决方案分析。

 Visual Studio Update 3 RC 包含增强的代码分析器诊断 v2 引擎，可显著减少内存使用量并缩短 CPU 空闲时间（即使启用了完整的解决方案分析）。
