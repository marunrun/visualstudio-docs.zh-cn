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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: df06a17ecc093cf24a64e7c3aa11a096a61ee44f
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63436840"
---
# <a name="how-to-enable-and-disable-full-solution-analysis-for-managed-code"></a>如何：启用和禁用托管代码的完整解决方案分析
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

备注
> 本主题仅适用于 Visual Studio 2015 Update 3 RC 和更高版本。  
  
 *完整解决方案分析*是 Visual Studio 功能，使你可以选择是否查看仅在打开 Visual C# 或 Visual Basic 文件在你的解决方案，或在解决方案中的打开和关闭 Visual C# 或 Visual Basic 文件中的代码分析问题。  
  
 尽管能够看到所有文件中的所有问题很有用，它可以是分散注意力，甚至减慢 Visual Studio，如果你的解决方案非常大或具有大量文件。  若要限制显示的问题数并改进 Visual Studio 性能，可以禁用完整解决方案分析。 如果您希望，可以轻松地重新启用此功能。  
  
#### <a name="to-toggle-full-solution-analysis"></a>若要切换完整解决方案分析  
  
1. 在 Visual Studio 中主菜单上，选择**工具** &#124; **选项**查看**选项**对话框。  
  
2. 在中**选项**对话框框中，选择**文本编辑器** &#124; **C#** 或**基本** &#124; **高级**.  
  
3. 选择**启用完整解决方案分析**复选框以启用完整解决方案分析或清除相应的框以禁用它。 选择**确定**按钮完成后。  
  
     ![启用完整解决方案分析复选框。](../code-quality/media/fsa-toolsoptions.png "FSA_ToolsOptions")  
  
## <a name="results-of-enabling-and-disabling-full-solution-analysis"></a>启用和禁用完整解决方案分析的结果  
 在以下屏幕截图中，您可以看到结果时启用完整解决方案分析。 所有错误和中的代码分析问题*所有*的解决方案中的文件显示，而不考虑文件是否都打开。  
  
 ![启用完整解决方案分析。](../code-quality/media/fsa-enabled.png "FSA_Enabled")  
  
 禁用完整解决方案分析之后，下面的屏幕截图显示同一解决方案中的结果。 仅将错误和代码分析问题，在错误列表中打开的解决方案文件会显示。  
  
 ![禁用完整解决方案分析。](../code-quality/media/fsa-disabled.png "FSA_Disabled")  
  
## <a name="automatically-disabling-full-solution-analysis"></a>自动禁用完整解决方案分析  
 如果 Visual Studio 检测到的 200 MB 或更少的系统内存可供它，它会自动禁用完整解决方案分析 （以及其他一些功能） 如果已启用。 如果发生这种情况，会显示警报，通知你这些。 按钮可以重新启用完整解决方案分析，如果你想要执行此操作。  
  
 ![警报文本中挂起完整解决方案分析](../code-quality/media/fsa-alert.png "FSA_Alert")  
  
## <a name="additional-details"></a>更多详细信息  
 默认情况下，完整解决方案分析适用于 Visual Basic 启用和禁用对于 Visual C#。  
  
 Visual Studio Update 3 RC 包括增强的代码分析工具诊断 v2 引擎，大大减少内存使用情况和减少 CPU 时间空闲，即使启用完整解决方案分析。
