---
title: 快速入门： C 的代码分析-C++ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
helpviewer_keywords:
- C/C++ code analysis
- code analysis,C/C++
ms.assetid: 6110b8ba-0af6-4acd-b1ba-bb0551f90e44
caps.latest.revision: 10
author: corob-msft
ms.author: corob
manager: jillfra
ms.openlocfilehash: e9db06ec0748ce4499afb423fac03886cd763301
ms.sourcegitcommit: 68f893f6e472df46f323db34a13a7034dccad25a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2020
ms.locfileid: "77278479"
---
# <a name="quick-start-code-analysis-for-cc"></a>快速入门：C/C++ 代码分析
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以通过常规地运行C 或 C++ 代码的代码分析以提高应用程序的质量。 这可帮助你查找常见问题、良好编程习惯的违例，或者很难通过测试发现的缺陷。 代码分析警告与编译器错误和警告不同，因为代码分析工具搜索的是虽然有效但仍会为你或使用你代码的其他人员带来问题的特定代码模式。  
  
## <a name="in-this-topic"></a>本主题内容  
  
- [为项目配置规则集](../code-quality/quick-start-code-analysis-for-c-cpp.md#BKMK_ConfigureRuleSets)  
  
- [运行代码分析](../code-quality/quick-start-code-analysis-for-c-cpp.md#BKMK_Run)  
  
- [分析和解决代码分析警告](../code-quality/quick-start-code-analysis-for-c-cpp.md#BKMK_Analyze)  
  
- [禁止显示代码分析警告](../code-quality/quick-start-code-analysis-for-c-cpp.md#BKMK_Suppress)  
  
- [为代码分析警告创建工作项](../code-quality/quick-start-code-analysis-for-c-cpp.md#BKMK_Creating_work_items_for_code_analysis_warnings)  
  
- [搜索和筛选代码分析结果](../code-quality/quick-start-code-analysis-for-c-cpp.md#BKMK_Search)  
  
## <a name="BKMK_ConfigureRuleSets"></a>为项目配置规则集  
  
1. 在**解决方案资源管理器**中，打开项目名称的快捷菜单，然后选择 "**属性**"。  
  
2. 可选择执行以下步骤：  
  
    1. 在 "**配置**" 和 "**平台**" 列表中，选择生成配置和目标平台。  
  
    2. 默认情况下，代码分析不报告由外部工具自动生成的代码所产生的警告。 若要查看生成的代码中的警告，请清除 "**禁止显示生成代码的结果**" 复选框。  
  
        > [!NOTE]
        > 当生成的代码所产生的代码分析错误和警告出现在窗体和模板中时，此选项不会取消显示它们。 可以查看和维护窗体或模板的源代码。  
  
3. 若要在每次使用所选配置生成项目时运行代码分析，请选中 "对**生成启用代码C++分析**" 复选框。 还可以通过打开 "**分析**" 菜单，然后选择 "在*项目名称***上运行代码分析"** 来手动运行代码分析。  
  
4. 在 "**运行此规则集**" 列表中，执行下列操作之一：  
  
    - 选择要使用的规则集。  
  
    - 选择 **\<浏览 .。。>** 指定列表中不存在的现有自定义规则集。  
  
    - 定义自定义规则集。  
  
         有关详细信息，请参阅[创建自定义规则集](../code-quality/creating-custom-code-analysis-rule-sets.md)。  
  
### <a name="standard-cc-rule-sets"></a>标准的 C/C++ 规则集  
 Visual Studio 包括两个本机代码标准规则集：  
  
|规则集|说明|  
|--------------|-----------------|  
|Microsoft 本机最少量建议规则|此规则集重点关注本机代码中的最关键问题，包括潜在安全漏洞和应用程序故障。 应在你为本机项目创建的任何自定义规则集中包含此规则集。|  
|Microsoft 本机建议规则|此规则集涵盖多种问题。 它包括 Microsoft 本机最少量建议规则中的所有规则。|  
  
## <a name="BKMK_Run"></a>运行代码分析  
 在项目属性页的"代码分析"页中，你可以配置代码分析在每次生成项目时都运行。 还可手动运行代码分析。  
  
 对解决方案运行代码分析：  
  
- 在“生成”菜单上，选择“对解决方案运行代码分析”。  
  
  对项目运行代码分析：  
  
- 在“解决方案资源管理器”中，选择项目名称。  
  
- 在 "**生成**" 菜单上，选择 "对*项目名称***运行代码分析**"。  
  
  编译项目或解决方案，并运行代码分析。 结果将显示在“代码分析”窗口中。  
  
## <a name="BKMK_Analyze"></a>分析和解决代码分析警告  
 若要分析某个具体的警告，请在“代码分析”窗口中选择该警告的标题。 该警告展开以显示有关相关问题的其他信息。 如果可能，代码分析会显示行号，并分析导致该警告的逻辑。 有关该警告的详细信息（包括对问题的可能解决方案），请选择该警告 ID 以显示 MSND 库中该消息的帮助主题。  
  
 展开警告后，将在 Visual Studio 代码编辑器中突出显示导致警告的代码行。  
  
 了解问题后，可在代码中解决该问题。 然后重新运行代码分析，以确保警告不再显示在“代码分析”窗口中，并且修复未引发新的警告。  
  
> [!TIP]
> 可从“代码分析”窗口中重新运行代码分析。 选择 "**分析**" 按钮，然后选择分析的范围。 可对整个解决方案对所选项目重新运行分析。  
  
## <a name="BKMK_Suppress"></a>禁止显示代码分析警告  
 有时，你可能会决定不修复代码分析警告。 你可能会觉得与代码的任何真实实现中引发问题的可能性相比，解决警告所需的重新编码工作量过大。 或者，你可能会认为在警告中使用的分析不适合特定的上下文。 可禁止显示个别警告，以使“代码分析”窗口中不再显示这些警告。  
  
 若要禁止显示警告，请执行以下操作：  
  
1. 如果未显示详细信息，请选择警告标题将其展开。  
  
2. 选择警告底部的“操作”链接。  
  
3. 选择 "**禁止显示消息**"，然后选择 **"在源中"** 。  
  
   禁止显示消息会插入用于禁止显示代码行的警告的 `#pragma warning (disable:`*WarningId*`)`。  
  
## <a name="BKMK_Creating_work_items_for_code_analysis_warnings"></a>为代码分析警告创建工作项  
 可以使用 Visual Studio 中的工作项跟踪功能来记录 bug。 若要使用此功能，必须连接到 Team Foundation Server 的实例。  
  
 **为一个或多个 C/C++代码警告创建工作项**  
  
1. 在“代码分析”窗口中，展开并选择警告  
  
2. 在警告的快捷菜单上，选择 "**创建工作项**"，然后选择 "工作项类型"。  
  
3. Visual Studio 为选定的警告创建一个工作项，并在 IDE 的文档窗口中显示该工作项。  
  
4. 添加任何附加信息，然后选择 "**保存工作项**"。  
  
## <a name="BKMK_Search"></a>搜索和筛选代码分析结果  
 可搜索冗长的警告消息列表，也可在多项目解决方案中筛选警告。  
  
1. **按标题或警告 id 筛选警告**：在 "**筛选器**" 文本框中输入关键字。  
  
2. **按项目筛选警告**：在多项目解决方案中，在 "代码分析" 窗口右上角的列表中选择一个或多个项目。 选择要显示所有警告的解决方案名称。  
  
3. **按严重性筛选警告**：默认情况下，将为代码分析消息分配严重性 "**警告**"。 可以将一个或多个消息的严重性指定为自定义规则集中的**错误**。 选择 "**警告**" 或 "**错误**" 以仅显示分配了相应严重性的消息。 选择 "**全部**" 以显示所有消息。
