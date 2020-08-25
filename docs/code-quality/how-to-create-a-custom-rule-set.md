---
title: 创建自定义代码分析规则集
ms.date: 11/02/2018
ms.topic: how-to
f1_keywords:
- vs.codeanalysis.addremoverulesets
helpviewer_keywords:
- rule sets
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 643ee48f798c90851d5ff323685070f9d7268f04
ms.sourcegitcommit: a801ca3269274ce1de4f6b2c3f40b58bbaa3f460
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88801030"
---
# <a name="customize-a-rule-set"></a>自定义规则集

你可以创建自定义规则集来满足代码分析的特定项目需求。

## <a name="create-a-custom-rule-set-from-an-existing-rule-set"></a>基于现有规则集创建自定义规则集

若要创建自定义规则集，可以在 **规则集编辑器**中打开内置规则集。 在此处，你可以添加或删除特定的规则，并且可以更改违反规则时发生的操作 &mdash; （例如，显示警告或错误）。

1. 在 **解决方案资源管理器**中，选择并按住 (或右键单击项目) ，然后选择 " **属性**"。

2. 在 " **属性** " 页上，中转到 " **代码分析** " 选项卡。

::: moniker range="vs-2017"

3. 在 " **运行此规则集** " 下拉列表中，执行下列操作之一：

::: moniker-end

::: moniker range=">=vs-2019"

3. 在 " **活动规则** " 下拉列表中，执行下列操作之一：

::: moniker-end

   - 选择要自定义的规则集。

     \- 或 -

   - 选择 **\<Browse>** 此项可指定列表中不存在的现有规则集。

4. 选择 " **打开** " 以在规则集编辑器中显示规则。

> [!NOTE]
> 如果你有 .NET Core 或 .NET Standard 项目，该过程会稍有不同，因为没有 **代码分析** 属性选项卡。请按照以下步骤将 [预定义规则集复制到你的项目，并将其设置为活动规则集](analyzer-rule-sets.md)。 复制规则集之后，可以 [在 Visual Studio 规则集编辑器中进行编辑](working-in-the-code-analysis-rule-set-editor.md) ，方法是从 **解决方案资源管理器**中打开它。

## <a name="create-a-new-rule-set"></a>创建新规则集

您可以通过 " **新建文件** " 对话框创建新的规则集文件：

1. 选择**File**  >  **New**  >  "文件" "新建**文件**"，或选择**Ctrl** + **N**。

2. 在 " **新建文件** " 对话框中，选择左侧的 " **常规** " 类别，然后选择 " **代码分析规则集**"。

3. 选择“打开”  。

   *新的*文件组文件将在规则集编辑器中打开。

## <a name="create-a-custom-rule-set-from-multiple-rule-sets"></a>从多个规则集创建自定义规则集

> [!NOTE]
> 以下过程不适用于没有 **代码分析** 属性选项卡的 .net Core 项目。

1. 在 **解决方案资源管理器**中，选择并按住 (或右键单击项目) ，然后选择 " **属性**"。

2. 在 " **属性** " 页上，中转到 " **代码分析** " 选项卡。

::: moniker range="vs-2017"

3. 选择 **\<Choose multiple rule sets>** " **运行此规则集**"。

::: moniker-end

::: moniker range=">=vs-2019"

3. **\<Choose multiple rule sets>** 从**活动规则**中选择。

::: moniker-end

4. 在 " **添加或删除规则集** " 对话框中，选择要包括在新规则集中的规则集。

   !["添加或删除规则集" 对话框](media/add-remove-rule-sets.png)

5. 选择 " **另存为**"，输入 *. 规则* 文件文件的名称，然后选择 " **保存**"。

   此时将在 " **运行此规则集** " 列表中选择新规则集。

6. 选择 " **打开** " 以在规则集编辑器中打开新规则集。

## <a name="rule-precedence"></a>规则优先级

- 如果在具有不同严重性的规则集中多次列出相同的规则，则编译器将生成错误。 例如：

   ```xml
   <RuleSet Name="Rules for ClassLibrary21" Description="Code analysis rules for ClassLibrary21.csproj." ToolsVersion="15.0">
     <Rules AnalyzerId="Microsoft.Analyzers.ManagedCodeAnalysis" RuleNamespace="Microsoft.Rules.Managed">
       <Rule Id="CA1021" Action="Warning" />
       <Rule Id="CA1021" Action="Error" />
     </Rules>
   </RuleSet>
   ```

- 如果在具有 *相同* 严重性的规则集中多次列出相同的规则，则可能会在 **错误列表**中看到以下警告：

   **CA0063：无法加载规则集文件 " \[ 你的]. 规则集" 或其依赖规则集文件之一。此文件不符合规则集架构。**

- 如果规则集包括使用 **包含** 标记的子规则集，并且子规则和父规则集都列出相同的规则但严重性不同，则父规则集中的严重性优先。 例如：

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

## <a name="name-and-description"></a>名称和说明

若要更改编辑器中打开的规则集的显示名称，请在菜单栏上选择 "**查看**属性" 窗口以打开 "**属性**" 窗口  >  **Properties Window** 。 在 " **名称** " 框中输入显示名称。 还可以输入规则集的说明。

## <a name="next-steps"></a>后续步骤

现在，你已创建规则集，下一步是通过添加或删除规则或修改规则冲突的严重性来自定义规则。

> [!div class="nextstepaction"]
> [修改规则集编辑器中的规则](../code-quality/working-in-the-code-analysis-rule-set-editor.md)

## <a name="see-also"></a>请参阅

- [如何：配置托管代码项目的代码分析](../code-quality/how-to-configure-code-analysis-for-a-managed-code-project.md)
- [代码分析规则集参考](../code-quality/rule-set-reference.md)
