---
title: 配置托管代码的实时代码分析范围
ms.date: 03/23/2018
ms.topic: conceptual
helpviewer_keywords:
- live code analysis
- background analysis
- analysis scope
- full solution analysis
author: Mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 5b1e4362755bbbfa9ea220fcbdf92abf92723521
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2020
ms.locfileid: "85462118"
---
# <a name="how-to-configure-live-code-analysis-scope-for-managed-code"></a>如何：配置托管代码的实时代码分析范围

## <a name="what-is-live-code-analysis-for-managed-code"></a>托管代码的 "实时代码分析" 是什么？
当您在编辑器中编辑源文件时，Visual Studio 将执行一系列实时代码分析（也称为*后台分析*）。 其中的一些要求是可接受的 Visual Studio IDE 编辑体验的最小分析。 其中一些是为了改进 IDE 功能的响应能力。 尽管其中一些功能是启用其他 IDE 功能，如 Roslyn 分析器中的诊断和代码修补程序。 根据功能，可以将这些分析分组如下：

- **诊断的后台计算**：分析以计算源文件中的错误、警告和建议。 这些诊断显示为 "错误列表" 中的条目，在编辑器中显示为 "波形曲线"。 它们可以分为两个类别：
    - C # 和 Visual Basic 编译器诊断
    - Roslyn analyzer 诊断，其中包括：

        - 用于代码样式建议和的内置 IDE 分析器
        - 为当前解决方案中的项目[安装](./install-roslyn-analyzers.md)的第三方分析器包。

- **其他后台分析**：用于提高 IDE 功能的响应能力和 Visual Studio 交互的分析。 此类分析的一些示例包括：
    - 打开文件的后台分析。
    - 项目的后台编译，其中包含打开的文件以实现某些 IDE 功能的响应能力。
    - 构建语法和符号缓存。
    - 检测源文件的设计器关联，如窗体、控件等。

## <a name="default-analysis-scope"></a>默认分析范围

默认情况下，对于在 Visual Studio 中_打开_的所有文件，对诊断的后台计算执行实时代码分析。 上面提到的_其他一些后台分析_只对所有项目执行，其中至少有一个打开的文件。 虽然对整个解决方案执行的后台分析很少。

## <a name="custom-analysis-scope"></a>自定义分析范围

每个后台分析的默认作用域已经过优化，可以获得最佳的用户体验、功能以及大部分客户方案和解决方案的性能。 但是，在某些情况下，客户可能想要自定义此范围以减少或增加背景分析。 例如：

- 省电模式：如果用户在笔记本电脑电池上运行，则可能需要最大限度地减少电量消耗。 在这种情况下，他们需要将后台分析降到最低。
- 按需代码分析：如果用户更喜欢关闭实时分析器执行并按需手动运行代码分析，则需要将后台分析降到最低。 请参阅[如何：按需手动运行代码分析](./how-to-run-code-analysis-manually-for-managed-code.md)。
- 完整解决方案分析：如果用户想要始终查看解决方案中所有文件的所有诊断，无论它们是否已在编辑器中打开。 在此方案中，他们需要将后台分析范围最大化到整个解决方案。

从 Visual Studio 2019 版本16.5 开始，用户可以显式自定义适用于 c # 和 Visual Basic 项目的所有实时代码分析（包括诊断计算）的范围。 可用的分析范围包括：

- **当前文档**：将实时代码分析范围降到最低，以便仅对编辑器中的当前或可见文件执行。
- **打开文档**：默认的实时代码分析范围，如上一节所述。
- **整个解决方案**：将实时代码分析范围最大化，为整个解决方案中的所有文件和项目执行。

可以通过以下步骤在 "工具选项" 对话框中选择上述自定义分析范围之一：

1. 若要打开 "**选项**" 对话框，请在 Visual Studio 的菜单栏中选择 "**工具**" "  >  **选项**"。

2. 在 "**选项**" 对话框中，选择 "**文本编辑器**" "  >  **c #** " 或 "**基本**  >  **高级**"。

3. 选择所需的**后台分析范围**以自定义分析范围。 完成后，请选择 **"确定"** 。

![分析范围。](./media/background-analysis-scope.png)

> [!NOTE]
> 在 Visual Studio 2019 版本16.5 之前，用户可以使用 "**工具**" "选项" "文本编辑器" " **Enable full solution analysis**  >  **Options**  >  **Text Editor**  >  **c #** " 或 "**基本**  >  **高级**" 选项卡上的 "启用完整解决方案分析" 复选框，自定义用于诊断计算的分析范围。在之前的 Visual Studio 版本中不支持将后台分析范围降到最低。

## <a name="automatically-minimize-live-code-analysis-scope"></a>自动将实时代码分析范围降到最低

如果 Visual Studio 检测到可用于 200 MB 或更少的系统内存，它会自动将实时代码分析范围降到 "当前文档"。 如果出现这种情况，则会出现一个警报，通知你 Visual Studio 已禁用某些功能。 利用按钮，你可以在需要时切换回以前的分析范围。

![警报文本最小化分析范围](./media/fsa_alert.png)

## <a name="see-also"></a>请参阅

- [自动功能挂起](./automatic-feature-suspension.md)
- [省电模式功能请求](https://github.com/dotnet/roslyn/issues/38429)
