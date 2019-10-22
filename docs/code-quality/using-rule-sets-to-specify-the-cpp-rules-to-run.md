---
title: 使用规则集指定要运行的 C++ 规则
ms.date: 04/28/2018
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.rulesets.native
author: mikeblome
ms.author: mblome
manager: markl
ms.workload:
- cplusplus
ms.openlocfilehash: 8e25e28c2ff20a628058d5dfa71de0368fbe9249
ms.sourcegitcommit: 485ffaedb1ade71490f11cf05962add1718945cc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72445612"
---
# <a name="use-rule-sets-to-specify-the-c-rules-to-run"></a>使用规则集指定要运行C++的规则

在 Visual Studio 中，你可以创建和修改自定义*规则集*，以满足与代码分析相关的特定项目需求。 默认规则集存储在 `%VSINSTALLDIR%\Team Tools\Static Analysis Tools\Rule Sets` 中。

**Visual Studio 2017 版本15.7 及更高版本：** 你可以使用任何文本编辑器创建自定义规则集，并在命令行生成中应用它们，无论你使用的是何种生成系统。 有关详细信息，请参阅[/analyze：规则集](/cpp/build/reference/analyze-code-analysis)。

若要在 Visual C++ studio 中创建自定义规则集，必须C++在 visual Studio IDE 中打开 C/项目。 然后，在规则集编辑器中打开某一标准规则集，再添加或移除特定的规则，并且可更改当代码分析确定违反规则时所发生的操作。

若要创建新的自定义规则集，请使用新文件名进行保存。 自定义规则集会自动分配给项目。

## <a name="to-create-a-custom-rule-from-a-single-existing-rule-set"></a>基于单个现有规则集创建自定义规则

1. 在解决方案资源管理器中，打开项目的快捷菜单，然后选择 "**属性**"。

2. 在 "**属性**" 选项卡上，选择 "**代码分析**"。

3. 在 "**规则集**" 下拉列表中，执行下列操作之一：

   - 选择要自定义的规则集。

     \- 或 -

   - 选择 **\<Browse .。。>** 指定列表中不存在的现有规则集。

4. 选择 "**打开**" 以在规则集编辑器中显示规则。

## <a name="to-modify-a-rule-set-in-the-rule-set-editor"></a>在规则集编辑器中修改规则集

- 若要更改规则集的显示名称，请在 "**视图**" 菜单上选择 "**属性窗口**"。 在 "**名称**" 框中输入显示名称。 请注意，显示名称可能不同于文件名。

- 若要将组的所有规则添加到自定义规则集，请选中组的复选框。 若要删除组中的所有规则，请清除该复选框。

- 若要向自定义规则集添加特定规则，请选中该规则的复选框。 若要从规则集中删除规则，请清除该复选框。

- 若要更改在代码分析中违反规则时采取的操作，请选择该规则的 "**操作**" 字段，然后选择以下值之一：

     **警告**-生成警告。

     **错误**-生成错误。
     
     **Info** -生成一条消息。

     **无**-禁用规则。 此操作与从规则集中删除规则的操作相同。

## <a name="to-group-filter-or-change-the-fields-in-the-rule-set-editor-by-using-the-rule-set-editor-toolbar"></a>使用规则集编辑器工具栏对规则集编辑器中的字段进行分组、筛选或更改

- 若要展开所有组中的规则，请选择 "**全部展开**"。

- 若要折叠所有组中的规则，请选择 "**全部折叠**"。

- 若要更改对规则进行分组所依据的字段，请从 "**分组依据**" 列表中选择字段。 若要显示未分组的规则，请选择 **\<None >** 。

- 若要在规则列中添加或删除字段，请选择**列选项**。

- 若要隐藏不适用于当前解决方案的规则，请选择 "**隐藏不适用于当前解决方案的规则**"。

- 若要切换显示和隐藏分配了 "错误" 操作的规则，请选择 "**显示可以生成代码分析错误的规则**"。

- 若要切换显示和隐藏分配了 "警告" 操作的规则，请选择 "**显示可以生成代码分析警告的规则**"。

- 若要切换显示和隐藏分配了 "**无**" 操作的规则，请选择 "**显示未启用的规则**"。

- 若要添加或删除当前规则集的 Microsoft 默认规则集，请选择 "**添加或删除子规则集**"。

## <a name="to-create-a-rule-set-in-a-text-editor"></a>在文本编辑器中创建规则集

您可以在文本编辑器中创建自定义规则集，将其存储在具有 `.ruleset` 扩展名的任何位置，并使用[/analyze：规则集](/cpp/build/reference/analyze-code-analysis)编译器选项应用于。

下面的示例演示了一个基本规则集文件，你可以将其用作起始点：

::: moniker range="vs-2017"

```xml
<?xml version="1.0" encoding="utf-8"?>
<RuleSet Name="New Rule Set" Description=" " ToolsVersion="15.0">
  <Rules AnalyzerId="Microsoft.Analyzers.NativeCodeAnalysis" RuleNamespace="Microsoft.Rules.Native">
    <Rule Id="C6001" Action="Warning" />
    <Rule Id="C26494" Action="Warning" />
  </Rules>
</RuleSet>
```

::: moniker-end

::: moniker range=">=vs-2019"

```xml
<?xml version="1.0" encoding="utf-8"?>
<RuleSet Name="New Rule Set" Description=" " ToolsVersion="16.0">
  <Rules AnalyzerId="Microsoft.Analyzers.NativeCodeAnalysis" RuleNamespace="Microsoft.Rules.Native">
    <Rule Id="C6001" Action="Warning" />
    <Rule Id="C26494" Action="Warning" />
  </Rules>
</RuleSet>
```

::: moniker-end
