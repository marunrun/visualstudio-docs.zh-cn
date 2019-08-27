---
title: 使用规则集指定要运行的 C++ 规则
ms.date: 04/28/2018
ms.topic: conceptual
author: mikeblome
ms.author: mblome
manager: wpickett
ms.workload:
- cplusplus
ms.openlocfilehash: d4d7dfc1f010b860653edbe14fa7af9050bddba4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62820368"
---
# <a name="use-rule-sets-to-specify-the-c-rules-to-run"></a>使用规则集指定C++运行规则

在 Visual Studio 中，您可以创建和修改自定义*规则集*以满足与代码分析相关联的特定项目需求。 默认规则集存储在`%VSINSTALLDIR%\Team Tools\Static Analysis Tools\Rule Sets`。

**Visual Studio 2017 版本 15.7 及更高版本**可以创建自定义规则集使用任何文本编辑器，并将其应用在命令行生成，无论您使用的系统生成什么内容。 有关详细信息，请参阅[/analyze: ruleset](/cpp/build/reference/analyze-code-analysis)。

若要创建自定义C++规则集在 Visual Studio 中，C /C++必须在 Visual Studio IDE 中打开项目。 然后，在规则集编辑器中打开某一标准规则集，再添加或移除特定的规则，并且可更改当代码分析确定违反规则时所发生的操作。

若要创建新的自定义规则集，通过使用新的文件名保存。 自定义规则集自动分配给项目。

## <a name="to-create-a-custom-rule-from-a-single-existing-rule-set"></a>若要从单个的现有规则集创建自定义规则

1. 在解决方案资源管理器，打开项目的快捷菜单，然后选择**属性**。

2. 上**属性**选项卡上，选择**代码分析**。

3. 在中**规则集**下拉列表中，执行下列任一操作：

   - 选择要自定义的规则集。

     \- 或 -

   - 选择 **\<浏览...>** 指定的现有规则集不在列表中。

4. 选择**打开**若要在规则集编辑器中显示的规则。

## <a name="to-modify-a-rule-set-in-the-rule-set-editor"></a>若要修改的规则将设置规则集编辑器

- 若要更改在规则集的显示名称**视图**菜单中，选择**属性窗口**。 输入中的显示名称**名称**框。 请注意，显示名称可能不同于文件名称。

- 若要添加到自定义规则集的组的所有规则，请选择组的复选框。 若要删除的组的所有规则，请清除该复选框。

- 若要将特定的规则添加到自定义规则集，请选择规则的复选框。 若要从规则集中删除规则，请清除该复选框。

- 若要更改的代码分析中违反规则时执行的操作，请选择**操作**字段规则，然后选择以下值之一：

     **则发出警告**-生成警告。

     **错误**-将生成错误。

     **无**-禁用规则。 此操作是从规则集内移除规则相同的。

## <a name="to-group-filter-or-change-the-fields-in-the-rule-set-editor-by-using-the-rule-set-editor-toolbar"></a>要进行分组，筛选，或者通过使用规则集编辑器工具栏来更改规则集编辑器中的字段

- 若要展开所有组中的规则，请选择**全部展开**。

- 若要折叠所有组中的规则，请选择**折叠所有**。

- 若要更改规则分组所依据的字段，选择从字段**Group By**列表。 若要显示未分组的规则，请选择 **\<None >** 。

- 若要添加或删除字段，在规则列中，选择**列选项**。

- 若要隐藏不适用于当前解决方案的规则，请选择**隐藏不适用于当前解决方案的规则**。

- 若要切换显示和隐藏分配了错误操作的规则，请选择**显示可以生成代码分析错误的规则**。

- 若要切换显示和隐藏分配了警告操作规则，请选择**显示可以生成代码分析警告的规则**。

- 若要切换显示和隐藏分配了规则**无**操作中，选择**显示未启用的规则**。

- 若要添加或移除的 Microsoft 默认规则设置为当前的规则集，请选择**添加或移除子规则集**。

## <a name="to-create-a-rule-set-in-a-text-editor"></a>在文本编辑器中创建一个规则集

可以在文本编辑器创建自定义规则集，将其存储在任何位置`.ruleset`扩展，并使用应用[/analyze: ruleset](/cpp/build/reference/analyze-code-analysis)编译器选项。

下面的示例演示基本规则集文件，可以将作为起点：

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
