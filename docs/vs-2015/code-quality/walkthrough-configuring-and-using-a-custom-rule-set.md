---
title: 演练：配置和使用自定义规则集 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
helpviewer_keywords:
- code analysis, walkthroughs
- code analysis, rule sets
ms.assetid: 7fe0a4e3-1ce0-4f38-a87a-7d81238ec7cd
caps.latest.revision: 42
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 8239afd1cf4e8c0a5e702f2b0e4ed64408cada09
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72645742"
---
# <a name="walkthrough-configuring-and-using-a-custom-rule-set"></a>演练：配置和使用自定义规则集
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本演练演示如何使用已配置为对类库使用自定义 *规则集* 的代码分析工具。 你可以选择与你为解决方案指定的项目类型相关的规则集，也可以选择替代规则集来满足特定需求，例如扫描旧版代码以查找可以不间断地解决的问题。 在任一情况下，也可以自定义规则集，以便对其进行微调以满足项目要求。

 在本演练中，你将逐步完成以下过程：

- 创建类库。

- 选择 " **Microsoft 基本设计准则规则** " "代码分析规则集"。

- 向类添加您自己的代码。

- 运行代码分析。

- 自定义规则集。

- 运行代码分析并查看规则集自定义行为的工作方式。

## <a name="prerequisites"></a>先决条件

- [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)]、[!INCLUDE[vsPreLong](../includes/vsprelong-md.md)] 或 [!INCLUDE[vsPro](../includes/vspro-md.md)]

## <a name="using-rule-sets-with-code-analysis"></a>将规则集用于代码分析
 首先，创建一个简单的类库。

#### <a name="create-a-class-library"></a>创建类库

1. 在“文件”菜单上，单击“新建”，然后单击“项目”。

2. 在 " **新建项目** " 对话框中的 " **项目类型**" 下，单击 " **Visual c #**"。

3. 在 **Visual c #** 下 **，选择 "类库"**。

4. 在 " **名称** " 文本框中，键入 **RuleSetSample** ，然后单击 **"确定"**。

   接下来，选择 " **Microsoft 基本设计准则规则** " 规则集，并将其保存到项目中。

#### <a name="select-a-code-analysis-rule-set"></a>选择代码分析规则集

1. 在 " **分析** " 菜单上，单击 " **为 RuleSetSample 配置代码分析**"。

    将显示代码分析的配置设置。

2. 在 " **运行此规则集** " 下拉列表中，选择 " **Microsoft 所有规则**"。

    有关可用规则集的详细信息，请参阅 [代码分析规则集引用](../code-quality/code-analysis-rule-set-reference.md)。

    在 "文件" 菜单上，单击 " **保存选定项** " 以更新项目文件，其中包含有关所选规则集及其设置的信息。

   > [!TIP]
   > 在实际情况下，一种很好的做法是使用来确定要以代码分析为目标的问题的优先顺序，即从 **最小的建议规则** 集开始，并纠正所需的问题，然后以增量方式添加更多规则或规则集来查找和更正其他问题。

   接下来，您将向类库中添加一些代码，此代码将用于演示 CA1704 "标识符应拼写正确" 代码分析规则的冲突。 有关详细信息，请参阅 [CA1704：标识符应拼写正确](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)。

#### <a name="add-your-own-code"></a>添加自己的代码

- 在解决方案资源管理器中，打开 Class1.cs 文件并将现有代码替换为以下代码：

  ```
  using System;
  using System.Collections.Generic;
  using System.Text;

  namespace RuleSetSample
  {
      public class Class1
      {
          //The variable parameter names "a" and "b" will cause
          //the warning CA 1704 Microsoft.Naming "Consider
          //providing a more meaningful name" to fire
          public int AddIntegers(int a, int b)
          {

              int sum = a + b;

              return (sum);
          }
      }
  }

  ```

  现在，可以在 RuleSetSample 项目上运行代码分析，并查找错误列表窗口中生成的所有错误和警告。

#### <a name="run-code-analysis-on-the-rulesetsample-project"></a>对 RuleSetSample 项目运行代码分析

1. 在 " **分析** " 菜单上，单击 " **在 RuleSetSample 上运行代码分析**"。

2. 在 "错误列表" 窗口中，单击 " **警告** "，然后单击 " **说明** " 列标题以对警告 alphanumerically 进行排序。

    在实际应用程序中，你可以修复此时需要修复的任何规则冲突，或者可以根据需要关闭或取消规则（如果你确定不需要修复它）。 有关详细信息，请参阅[使用 SuppressMessage 特性禁止显示警告](../code-quality/suppress-warnings-by-using-the-suppressmessage-attribute.md)。

3. 请注意 CA1704 警告。 此规则上的这些冲突表明你应 "考虑为参数提供更有意义的名称。" 您可以在代码中更正问题，也可以禁用规则，如以下过程中所述。

   接下来，您将自定义规则集以排除 CA1704 警告 "标识符应正确拼写"。

#### <a name="customize-the-rule-set-for-your-project-to-disable-a-specific-rule"></a>为项目自定义规则集以禁用特定规则

1. 在 " **分析** " 菜单上，单击 " **为 RuleSetSample 配置代码分析**"。

2. 在 " **运行此规则集** " 下拉列表中，验证 " **Microsoft 所有规则** " 规则集仍为突出显示，然后单击 " **打开**"。 将显示 "规则集" 页。

3. 展开 "Microsoft. 命名类别" 节点，然后选择 "CA1704" 警告。

4. 在 " **操作** " 列下，选择 " **无"。** 这会阻止 CA1704 在 "错误列表" 窗口中显示为警告或错误。

    现在可以使用各种工具栏按钮和筛选选项来熟悉它们。 例如，您可以使用 " **分组依据** " 下拉列表来帮助查找特定规则或规则类别。 另一个示例是，可以使用 "规则集页面" 工具栏中的 " **隐藏禁用的规则** " 按钮，隐藏或显示 " **操作** " 列设置为 " **无**" 的所有规则。 如果要扫描已关闭的任何规则，以验证是否仍要禁用这些规则，这会很有用。

5. 在“视图”菜单上，单击“属性窗口”。 在 "属性" 工具窗口的 "名称" 框中键入 **"我的自定义规则集** "。 这会更改 IDE 中新规则集的显示名称 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 。

6. 在 " **文件** " 菜单上，单击 " **保存 Microsoft 所有规则** " 以保存自定义规则集。 导航到项目的根文件夹。 在 **"文件名"** 文本框中，键入 **MyCustomRuleSet**。 现在可以选择自定义规则集用于项目。

   创建新规则集后，必须配置项目设置以指定你要将新规则集用于该规则集。

#### <a name="specify-the-new-rule-set-for-use-with-your-project"></a>指定与项目一起使用的新规则集

1. 在解决方案资源管理器中，右键单击项目，然后选择 " **属性**"。

2. 在 " **属性** " 选项卡中，单击 " **代码分析**"。

    在 " **运行此规则集** " 下拉列表中，单击 "" **\<Browse..>** 。 导航到代码项目的根文件夹，然后选择 " **MyCustomRuleSet**"。 这是你在前面的过程中创建的新规则集。

3. 在 " **文件** " 菜单上，单击 " **保存** " 以保存项目配置。 现在可将自定义规则集用于项目。

   最后，你将使用 MyCustomRuleSet 规则集再次运行代码分析。 请注意，"错误列表" 窗口不显示 CA1704 性能规则冲突。

#### <a name="run-code-analysis-on-the-rulesetsample-project-for-the-second-time"></a>第二次在 RuleSetSample 项目上运行代码分析

1. 在 " **分析** " 菜单上，单击 " **在 RuleSetSample 上运行代码分析**"。

2. 请注意，在 "错误列表" 窗口中单击 " **警告**" 时，将不再看到 "标识符应正确拼写" 规则的 CA1704 警告冲突。

## <a name="see-also"></a>另请参阅
 [如何：配置托管代码的代码分析项目](../code-quality/how-to-configure-code-analysis-for-a-managed-code-project.md)[代码分析规则集引用](../code-quality/code-analysis-rule-set-reference.md)
