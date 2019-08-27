---
title: 创建自定义代码分析规则集
ms.date: 11/02/2018
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.addremoverulesets
helpviewer_keywords:
- rule sets
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f2f642ea8e41e4a9ccf2b35f432df528fc5e81d0
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65676563"
---
# <a name="customize-a-rule-set"></a>自定义规则集

可以创建自定义规则集以满足代码分析的特定项目需求。

## <a name="create-a-custom-rule-set-from-an-existing-rule-set"></a>创建自定义规则集从现有的规则集

若要创建自定义规则集，则可以打开所设置的内置规则**规则集编辑器**。 在这里，您可以添加或删除的特定规则，并且你可以更改时执行的操作违反规则&mdash;例如，显示一条警告或错误。

1. 在中**解决方案资源管理器**，右键单击项目，然后选择**属性**。

2. 上**属性**页中，选择**代码分析**选项卡。

3. 在中**运行此规则集**下拉列表中，执行下列任一操作：

   - 选择想要自定义的规则集。

     \- 或 -

   - 选择 **\<浏览...>** 指定的现有规则集不在列表中。

4. 选择**打开**若要在规则集编辑器中显示的规则。

> [!NOTE]
> 如果您有一个.NET Core 或.NET Standard 项目，该过程与稍有不同，因为没有任何**代码分析**属性选项卡。请按照步骤进行[复制预定义的规则设置为你的项目并将其设置为活动规则集](analyzer-rule-sets.md)。 您已复制的规则集后，你可以[在 Visual Studio 规则集编辑器中编辑它](working-in-the-code-analysis-rule-set-editor.md)通过打开从**解决方案资源管理器**。

## <a name="create-a-new-rule-set"></a>创建新的规则集

可以创建新的规则集文件从**新的文件**对话框：

1. 选择**文件** > **新建** > **文件**，或按**Ctrl**+**N**.

2. 在**新的文件**对话框中，选择**常规**左边的类别，然后选择**代码分析规则集**。

3. 选择“打开”  。

   新 *.ruleset*规则集编辑器中打开文件。

## <a name="create-a-custom-rule-set-from-multiple-rule-sets"></a>创建自定义规则集从多个规则集

> [!NOTE]
> 下面的过程不适用于.NET Core 项目，没有**代码分析**属性选项卡。

1. 在中**解决方案资源管理器**，右键单击项目，然后选择**属性**。

2. 上**属性**页中，选择**代码分析**选项卡。

3. 选择 **\<选择多个规则集...>** 从 **运行此规则集** 。

4. 在中**添加或删除规则集**对话框中，选择规则集你想要包括在新的规则集。

   ![添加或删除规则集对话框](media/add-remove-rule-sets.png)

5. 选择**另存为**，输入的名称 *.ruleset*文件，并选择**保存**。

   中选择新的规则集**运行此规则集**列表。

6. 选择**打开**以打开新的规则集编辑器中设置的规则。

## <a name="rule-precedence"></a>规则优先顺序

- 如果相同的规则是列出两个或更多次的规则集具有不同的严重级别中，编译器将生成错误。 例如：

   ```xml
   <RuleSet Name="Rules for ClassLibrary21" Description="Code analysis rules for ClassLibrary21.csproj." ToolsVersion="15.0">
     <Rules AnalyzerId="Microsoft.Analyzers.ManagedCodeAnalysis" RuleNamespace="Microsoft.Rules.Managed">
       <Rule Id="CA1021" Action="Warning" />
       <Rule Id="CA1021" Action="Error" />
     </Rules>
   </RuleSet>
   ```

- 如果相同的规则是列出两个或更多次在规则集与*同一*严重性，可能会看到以下警告**错误列表**:

   **CA0063:未能加载规则集文件\[你].ruleset 或其依赖规则之一将设置文件。该文件不符合规则集架构。**

- 如果规则集包含子规则集通过使用**Include**标记和子与父规则集列出相同的规则，但具有不同严重级别，然后在父规则集严重性优先。 例如：

   ```xml
   <!-- Parent rule set -->
   <?xml version="1.0" encoding="utf-8"?>
   <RuleSet Name="Rules for ClassLibrary21" Description="Code analysis rules for ClassLibrary21.csproj." ToolsVersion="15.0">
     <Include Path="classlibrary_child.ruleset" Action="Default" />
     <Rules AnalyzerId="Microsoft.Analyzers.ManagedCodeAnalysis" RuleNamespace="Microsoft.Rules.Managed">
       <Rule Id="CA1021" Action="Warning" /> <!-- Overrides CA1021 severity from child rule set -->
     </Rules>
   </RuleSet>

   <!-- Child rule set -->
   <?xml version="1.0" encoding="utf-8"?>
   <RuleSet Name="Rules from child" Description="Code analysis rules from child." ToolsVersion="15.0">
     <Rules AnalyzerId="Microsoft.Analyzers.ManagedCodeAnalysis" RuleNamespace="Microsoft.Rules.Managed">
       <Rule Id="CA1021" Action="Error" />
     </Rules>
   </RuleSet>
   ```

## <a name="name-and-description"></a>名称和描述

若要更改编辑器中打开的规则集的显示名称，打开**属性**通过选择窗口**视图** > **属性窗口**菜单栏上。 输入中的显示名称**名称**框。 您还可以输入规则集的说明。

## <a name="next-steps"></a>后续步骤

现在，已设置的规则下, 一步是自定义的规则，通过添加或删除规则或修改规则冲突的严重性。

> [!div class="nextstepaction"]
> [修改规则集编辑器中的规则](../code-quality/working-in-the-code-analysis-rule-set-editor.md)

## <a name="see-also"></a>请参阅

- [如何：配置托管的代码项目的代码分析](../code-quality/how-to-configure-code-analysis-for-a-managed-code-project.md)
- [代码分析规则集参考](../code-quality/rule-set-reference.md)