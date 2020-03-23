---
title: 为托管代码配置实时代码分析范围
ms.date: 03/23/2018
ms.topic: conceptual
helpviewer_keywords:
- live code analysis
- background analysis
- analysis scope
- full solution analysis
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 300e3f276a45cfe2115311c7d27eedce365616cf
ms.sourcegitcommit: 92361aac3665a934faa081e1d1ea89a067b01c5b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/17/2020
ms.locfileid: "79432089"
---
# <a name="how-to-configure-live-code-analysis-scope-for-managed-code"></a>如何：为托管代码配置实时代码分析范围

## <a name="what-is-live-code-analysis-for-managed-code"></a>什么是托管代码的"实时代码分析"？
Visual Studio 执行大量实时代码分析，也称为*背景分析*，同时在编辑器中编辑源文件。 对于可接受的可视化工作室 IDE 编辑体验，其中一些需要最少的分析。 其中一些是为了提高 IDE 功能的响应能力。 虽然其中一些功能是为了启用其他 IDE 功能，例如来自 Roslyn 分析器的诊断和代码修复。 根据功能，这些分析可以按如下方式分组：

- **诊断的后台计算**：分析以计算源文件中的错误、警告和建议。 这些诊断程序在错误列表中显示为条目，并在编辑器中显示。 它们可以分为两类：
    - C# 和可视化基本编译器诊断
    - 罗斯林分析仪诊断，包括：

        - 内置 IDE 分析器，用于代码样式建议和
        - 为当前解决方案中的项目[安装](./install-roslyn-analyzers.md)的第三方分析器包。

- **其他背景分析**：分析，以提高IDE功能的响应性和可视化工作室交互。 这种分析的一些例子包括：
    - 打开文件的背景分析。
    - 具有打开文件的项目的后台编译，以实现某些 IDE 功能的响应能力提高的符号。
    - 构建语法和符号缓存。
    - 检测源文件的设计器关联，如窗体、控件等。

## <a name="default-analysis-scope"></a>默认分析范围

默认情况下，对 Visual Studio 中_打开_的所有文件执行用于诊断后台计算的实时代码分析。 上面提到的_其他背景分析_很少对所有项目执行，这些项目至少有一个打开的文件。 虽然对整个解决方案执行的背景分析很少。

## <a name="custom-analysis-scope"></a>自定义分析范围

已针对大多数客户方案和解决方案优化了每个背景分析的默认范围，以实现最佳的用户体验、功能和性能。 但是，在某些情况下，客户可能希望自定义此范围以减少或增加背景分析。 例如：

- 节能模式：如果用户使用笔记本电脑电池运行，他们可能希望将功耗降至最低，从而延长电池使用时间。 在这种情况下，他们希望最小化后台分析。
- 按需代码分析：如果用户喜欢关闭实时分析器执行并按需手动运行代码分析，则他们希望将后台分析降至最低。 请参阅[操作方式：按需手动运行代码分析](./how-to-run-code-analysis-manually-for-managed-code.md)。
- 完整解决方案分析：如果用户希望始终查看解决方案中的所有文件中的所有诊断，无论它们是否在编辑器中打开。 在这种情况下，他们希望将后台分析范围最大化到整个解决方案。

从 Visual Studio 2019 版本 16.5 开始，用户可以显式自定义 C# 和 Visual Basic 项目的所有实时代码分析的范围，包括诊断计算。 可用的分析范围包括：

- **当前文档**：最小化实时代码分析范围，以便仅对编辑器中的当前或可见文件执行。
- **打开的文档**：默认实时代码分析范围，如上一节所述。
- **整个解决方案**：最大化实时代码分析范围，以执行整个解决方案中的所有文件和项目。

您可以通过以下步骤在"工具选项"对话框中选择上述自定义分析范围之一：

1. 要打开"**选项"** 对话框，在可视化工作室的菜单栏上选择 **"工具** > **选项**"。

2. 在"**选项**"对话框中，**选择文本编辑器** > **C#** 或**基本** > **高级**。

3. 选择所需的**背景分析范围**以自定义分析范围。 完成后选择 **"确定**"。

![分析范围。](./media/background-analysis-scope.png)

> [!NOTE]
> 在 Visual Studio 2019 版本 16.5 之前，用户可以使用 **"启用工具** > **选项** > **文本编辑器** > **C#** 或**基本** > **高级**"选项卡的 **"启用完整解决方案分析**"复选框，将诊断计算分析范围自定义到整个解决方案。不支持将以前的 Visual Studio 版本中的背景分析范围降至最低。

## <a name="automatically-minimize-live-code-analysis-scope"></a>自动最小化实时代码分析范围

如果 Visual Studio 检测到其可以使用 200 MB 或更少的系统内存，它会自动将实时代码分析范围最小化为"当前文档"。 如果发生这种情况，将显示一个警报，通知您 Visual Studio 已禁用某些功能。 如果需要，一个按钮允许您切换回以前的分析范围。

![警报文本最小化分析范围](./media/fsa_alert.png)

## <a name="see-also"></a>另请参阅

- [自动功能挂起](./automatic-feature-suspension.md)
- [节能模式功能请求](https://github.com/dotnet/roslyn/issues/38429)
