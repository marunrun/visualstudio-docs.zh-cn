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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: fa3a91df779094e3e11722dfc7bfc03c58bcea7e
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383410"
---
# <a name="walkthrough-configuring-and-using-a-custom-rule-set"></a>演练：配置和使用自定义规则集
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本演练演示如何使用已配置为使用自定义的代码分析工具*规则集*类库。 可以选择与您的解决方案，为指定，也可以选择的项目类型替代的规则集来满足特定需求例如扫描可以不间断的方式修复问题的旧代码的规则集。 在任一情况下，规则集还可以定制为你的项目要求微调。  
  
 在本演练中，将逐步完成以下过程：  
  
- 创建一个类库。  
  
- 选择**Microsoft 基本设计准则规则**代码分析规则集。  
  
- 将你自己的代码添加到类。  
  
- 运行代码分析。  
  
- 自定义规则集。  
  
- 运行代码分析，请参阅如何设置自定义行为的工作方式的规则。  
  
## <a name="prerequisites"></a>系统必备  
  
- [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)]、[!INCLUDE[vsPreLong](../includes/vsprelong-md.md)] 或 [!INCLUDE[vsPro](../includes/vspro-md.md)]  
  
## <a name="using-rule-sets-with-code-analysis"></a>使用规则集对代码分析  
 首先，创建一个简单的类库。  
  
#### <a name="create-a-class-library"></a>创建一个类库  
  
1. 在 **文件** 菜单上，单击 **新建** ，然后单击 **项目**。  
  
2. 在中**新的项目**对话框中的**项目类型**，单击**Visual C#** 。  
  
3. 下**Visual C#** ，选择**类库**。  
  
4. 在中**名称**文本框中，键入**RuleSetSample** ，然后单击**确定**。  
  
   接下来，将选择**Microsoft 基本设计准则规则**规则集，并将其保存在你的项目。  
  
#### <a name="select-a-code-analysis-rule-set"></a>选择代码分析规则集  
  
1. 上**分析**菜单上，单击**RuleSetSample 的配置代码分析**。  
  
    显示代码分析的配置设置。  
  
2. 在中**运行此规则集**下拉列表中，选择**Microsoft 的所有规则**。  
  
    有关可用的规则集的详细信息，请参阅[代码分析规则集引用](../code-quality/code-analysis-rule-set-reference.md)。  
  
    在文件菜单上单击**保存选定项**使用所选规则集有关的信息和其设置更新项目文件。  
  
   > [!TIP]
   > 在实际情况下，为了优先处理你想要针对的代码分析的问题的好办法是首先**最少量建议规则**规则集和更正所需的问题，以及如何以增量方式将要查找和更正的其他问题的更多的规则集。  
  
   接下来，会将一些代码添加到类库，用于演示 CA1704 冲突"的标识符应正确拼写"代码分析规则。 有关详细信息，请参阅[CA1704:标识符应正确拼写](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)。  
  
#### <a name="add-your-own-code"></a>添加你自己的代码  
  
- 在解决方案资源管理器中打开 Class1.cs 文件和现有代码替换为以下：  
  
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
  
  现在可以对 RuleSetSample 项目运行代码分析，并查找任何错误和警告错误列表窗口中生成。  
  
#### <a name="run-code-analysis-on-the-rulesetsample-project"></a>对 RuleSetSample 项目运行代码分析  
  
1. 上**分析**菜单上，单击**RuleSetSample 对运行代码分析**。  
  
2. 在错误列表窗口中，单击**警告**，然后单击**说明**列标题进行排序警告进行排序。  
  
    在实际应用程序中，你修复值得在此情况下，修复任何规则冲突或 （可选） 关闭或取消一条规则，如果你确定它值得修复不是。 有关详细信息，请参阅[使用 SuppressMessage 特性禁止显示警告](../code-quality/suppress-warnings-by-using-the-suppressmessage-attribute.md)。  
  
3. 请注意 CA1704 警告。 此规则的这些冲突指示应"考虑的一个更有意义的名称的参数。" 无法在代码中更正此问题或下一个过程中所述，可以禁用该规则。  
  
   接下来，将自定义规则集以排除 CA1704 警告，"标识符应正确拼写"。  
  
#### <a name="customize-the-rule-set-for-your-project-to-disable-a-specific-rule"></a>自定义规则集为你的项目禁用特定规则  
  
1. 上**分析**菜单上，单击**RuleSetSample 的配置代码分析**。  
  
2. 在中**运行此规则集**下拉列表中，验证**Microsoft 的所有规则**规则集仍会突出显示，然后单击**打开**。 将显示的规则组页。  
  
3. 展开 Microsoft.Naming 类别节点，然后选择 CA1704 警告。  
  
4. 下**操作**列中，选择**None。** 这可以防止 CA1704 作为警告或错误错误列表窗口中的显示。  
  
    现在将试验各种工具栏按钮的好时机和筛选选项以熟悉它们。 例如，可以使用**Group By**下拉列表来帮助查找特定规则的类别。 另一个示例是，可以使用**隐藏已禁用的规则**隐藏或显示与所有规则规则集页工具栏中的按钮**操作**列设置为**None**。 这很有用，如果你想要扫描的已关闭以验证你仍想要让他们禁用任何规则。  
  
5. 在视图菜单上单击属性窗口。 类型**我的自定义规则集**属性工具窗口的名称框中。 这会更改新规则中设置的显示名称[!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]IDE。  
  
6. 上**文件**菜单上，单击**保存 Microsoft 所有 Rules.ruleset**若要保存你的自定义的规则集。 导航到你的项目的根文件夹。 在中**文件名**文本框中，键入**MyCustomRuleSet**。 自定义规则集现在可以选择用于你的项目。  
  
   使用创建新规则集后，现在必须配置项目设置以指定你想要使用新规则与之设置。  
  
#### <a name="specify-the-new-rule-set-for-use-with-your-project"></a>指定设置以用于与你的项目的新规则  
  
1. 在解决方案资源管理器，右键单击项目，然后选择**属性**。  
  
2. 在中**属性**选项卡上，单击**代码分析**。  
  
    在中**运行此规则集**下拉列表中，单击 **\<浏览...>** 。 导航到你的代码项目的根文件夹，然后选择**MyCustomRuleSet.ruleset**。 这是在上一过程中创建的新规则集。  
  
3. 上**文件**菜单上，单击**保存**以保存项目配置。 自定义规则集现在可与你的项目。  
  
   最后，将运行代码分析再次使用 MyCustomRuleSet 规则集。 请注意，错误列表窗口不会显示 CA1704 性能规则冲突。  
  
#### <a name="run-code-analysis-on-the-rulesetsample-project-for-the-second-time"></a>第二次对 RuleSetSample 项目运行代码分析  
  
1. 上**分析**菜单上，单击**RuleSetSample 对运行代码分析**。  
  
2. 在错误列表窗口中，请注意，当您单击**警告**，不会再看到"标识符应正确拼写"规则冲突的 CA1704 警告。  
  
## <a name="see-also"></a>请参阅  
 [如何：配置托管的代码项目的代码分析](../code-quality/how-to-configure-code-analysis-for-a-managed-code-project.md)   
 [代码分析规则集参考](../code-quality/code-analysis-rule-set-reference.md)
