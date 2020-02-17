---
title: 快速入门：C/C++ 代码分析
description: 在 Visual Studio 中C++对代码运行静态分析，以检测常见的编码问题和缺陷。
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- C/C++ code analysis
- code analysis,C/C++
author: corob-msft
ms.author: corob
manager: markl
ms.workload:
- cplusplus
ms.openlocfilehash: 41d5c5a5ea966d1e092e7038d2fc3734c9bd9f15
ms.sourcegitcommit: 68f893f6e472df46f323db34a13a7034dccad25a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2020
ms.locfileid: "77272318"
---
# <a name="quickstart-code-analysis-for-cc"></a>快速入门：C/C++ 代码分析

可以通过常规地运行C 或 C++ 代码的代码分析以提高应用程序的质量。 这可帮助你查找常见问题、良好编程习惯的违例，或者很难通过测试发现的缺陷。 代码分析警告与编译器错误和警告不同，因为代码分析工具搜索的是虽然有效但仍会为你或使用你代码的其他人员带来问题的特定代码模式。

## <a name="configure-rule-sets-for-a-project"></a>配置项目的规则集

1. 在**解决方案资源管理器**中，打开项目名称的快捷菜单，然后选择 "**属性**"。

2. 根据需要，在 "**配置**" 和 "**平台**" 列表中，选择生成配置和目标平台。

3. 若要在每次使用所选配置生成项目时运行代码分析，请选中 "**生成时启用代码分析**" 复选框。 还可以通过打开 "**分析**" 菜单，然后选择 "对*项目名称***运行代码分析**" 或 **"对文件运行代码分析"** ，手动运行代码分析。

4. 选择要使用的[规则集](../code-quality/using-rule-sets-to-specify-the-cpp-rules-to-run.md)或创建[自定义规则集](../code-quality/how-to-create-a-custom-rule-set.md)。 如果使用 LLVM/clang-cl，请参阅[在 Visual Studio 中使用 clang](../code-quality/clang-tidy.md)来配置 clang 整理的分析选项。

### <a name="standard-cc-rule-sets"></a>标准的 C/C++ 规则集

Visual Studio 包括两个本机代码标准规则集：

|规则集|说明|
|--------------|-----------------|
|Microsoft 本机最少量建议规则|此规则集重点关注本机代码中的最关键问题，包括潜在安全漏洞和应用程序故障。 应在你为本机项目创建的任何自定义规则集中包含此规则集。|
|Microsoft 本机建议规则|此规则集涵盖多种问题。 它包括 Microsoft 本机最少量建议规则中的所有规则。|

## <a name="run-code-analysis"></a>运行代码分析

在项目属性页的 "代码分析" 页上，您可以将代码分析配置为每次生成项目时运行。 还可手动运行代码分析。

对解决方案运行代码分析：

- 在 "**生成**" 菜单中，选择 **"对解决方案运行代码分析**"。

对项目运行代码分析：

1. 在解决方案资源管理器中，选择项目的名称。

2. 在 "**生成**" 菜单中，选择 "对*项目名称***运行代码分析"** 。

对文件运行代码分析：

1. 在解决方案资源管理器中，选择文件的名称。

2. 在 "**生成**" 菜单中，选择 **"对文件运行代码分析**" 或按**Ctrl + Shift + Alt + F7**。

   编译项目或解决方案，并运行代码分析。 结果显示在错误列表中。

## <a name="analyze-and-resolve-code-analysis-warnings"></a>分析和解决代码分析警告

若要分析特定警告，请在错误列表中选择警告的标题。 该警告展开以显示有关相关问题的其他信息。 如果可能，代码分析会显示行号，并分析导致该警告的逻辑。 有关该警告的详细信息，包括问题的可能解决方案，请选择警告 ID 以显示其对应的联机帮助主题。

选择警告时，将在 Visual Studio 代码编辑器中突出显示导致警告的代码行。

了解问题后，可在代码中解决该问题。 然后，重新运行代码分析，以确保警告不再出现在错误列表中，并且修复未引发任何新的警告。

## <a name="suppress-code-analysis-warnings"></a>禁止显示代码分析警告

有时，你可能会决定不修复代码分析警告。 你可能会觉得与代码的任何真实实现中引发问题的可能性相比，解决警告所需的重新编码工作量过大。 或者，你可能会认为在警告中使用的分析不适合特定的上下文。 您可以禁止显示个别警告，使其不再出现在错误列表中。

若要禁止显示警告，请执行以下操作：

1. 如果未显示详细信息，请选择警告标题将其展开。

2. 选择警告底部的“操作”链接。

3. 选择 "**禁止显示消息**"，然后选择 **"在源中"** 。

   禁止显示消息会插入禁止显示代码行警告的 `#pragma warning (disable:[warning ID])`。

## <a name="create-work-items-for-code-analysis-warnings"></a>为代码分析警告创建工作项

可以使用 Visual Studio 中的工作项跟踪功能来记录 bug。 若要使用此功能，必须连接到 Team Foundation Server 的实例。

**为一个或多个 C/C++代码警告创建工作项**

1. 在错误列表中，展开并选择警告

2. 在警告的快捷菜单上，选择 "**创建工作项**"，然后选择 "工作项类型"。

3. Visual Studio 为选定的警告创建一个工作项，并在 IDE 的文档窗口中显示该工作项。

4. 添加任何附加信息，然后选择 "**保存工作项**"。

## <a name="search-and-filter-code-analysis-results"></a>搜索和筛选代码分析结果

可搜索冗长的警告消息列表，也可在多项目解决方案中筛选警告。

- **按标题或警告 ID 筛选警告**：在搜索框中输入关键字。

- **按严重性筛选警告**：默认情况下，将为代码分析消息分配严重性 "**警告**"。 可以将一个或多个消息的严重性指定为自定义规则集中的**错误**。 在**错误列表**的 "**严重性**" 列中，选择下拉箭头，然后选择 "筛选器" 图标。 选择 "**警告**" 或 "**错误**" 以仅显示分配了相应严重性的消息。 选择 "全**选**" 以显示所有消息。

## <a name="see-also"></a>另请参阅

- [C/的代码分析C++](../code-quality/code-analysis-for-c-cpp-overview.md)
