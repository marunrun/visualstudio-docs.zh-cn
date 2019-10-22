---
title: 如何：创建自定义规则集 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.addremoverulesets
helpviewer_keywords:
- Development Edition, rule sets
ms.assetid: bcc42508-9592-4802-9f66-a50111641d73
caps.latest.revision: 26
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 6e4aef02a2bb320112d7d268da28cf66b1ec6751
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72657450"
---
# <a name="how-to-create-a-custom-rule-set"></a>如何：创建自定义规则集
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 [!INCLUDE[vsUltShort](../includes/vsultshort-md.md)]、[!INCLUDE[vsPreShort](../includes/vspreshort-md.md)] 和 [!INCLUDE[vsPro](../includes/vspro-md.md)]，可以创建和修改自定义*规则集*，以满足与代码分析相关的特定项目需求。 若要创建自定义规则集，请在规则集编辑器中打开一个或多个标准规则集。 然后，你可以添加或删除特定的规则，并且可以更改代码分析确定违反规则时发生的操作。

 若要创建新的自定义规则集，请使用新文件名进行保存。 自定义规则集会自动分配给项目。

## <a name="opening-the-rule-set-editor"></a>打开规则集编辑器

#### <a name="to-open-an-empty-rule-set-file-in-the-rule-set-editor"></a>在规则集编辑器中打开一个空的规则集文件

1. 在 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 的 "**文件**" 菜单上，指向 "**新建**"，然后单击 "**文件**"。

2. 在 "**新建文件**" 对话框中，单击 "**已安装的模板**" 列表中的 "**常规**"，然后选择 "**代码分析规则集**"。

3. 此时将显示 "规则集编辑器"。 编辑器列表中未选择任何规则。

#### <a name="to-create-a-custom-rule-from-a-single-existing-rule-set"></a>基于单个现有规则集创建自定义规则

1. 在解决方案资源管理器中，右键单击项目，然后选择 "**属性**"。

2. 在 "**属性**" 选项卡上，单击 "**代码分析**"。

3. 在 "**规则集**" 下拉列表中，执行下列操作之一：

   - 选择要自定义的规则集。

     \- 或 -

   - 选择 **\<Browse .。。>** 指定列表中不存在的现有规则集。

4. 单击 "**打开**" 以在规则集编辑器中显示规则。

#### <a name="to-create-a-custom-rule-set-from-multiple-existing-rule-sets"></a>从多个现有规则集创建自定义规则集

1. 在解决方案资源管理器中，右键单击项目，然后选择 "**属性**"。

2. 在 "**属性**" 选项卡上，单击 "**代码分析**"。

3. 选择 **\<Choose 多个规则集 .。。>** **运行此规则集**。

4. 在 "**添加或删除规则集**" 对话框中，选择要基于其新建规则集的规则集，然后单击 **"确定"** 。

5. 保存新规则集。

     在 "**运行此规则集**" 列表中选择新规则集的名称。 您可以在下一步中更改规则集的显示名称。

6. 可有可无若要更改规则集的显示名称，请在 "**视图**" 菜单上单击 "**属性窗口**"。 在 "**名称**" 框中键入显示名称。

7. 若要添加、删除或修改新规则集中的特定代码分析规则，请单击 "**打开**"。

## <a name="modifying-a-rule-set"></a>修改规则集

#### <a name="to-modify-a-rule-set-in-the-rule-set-editor"></a>在规则集编辑器中修改规则集

- 若要更改规则集的显示名称，请在 "**视图**" 菜单上单击 "**属性窗口**"。 在 "**名称**" 框中输入显示名称。 请注意，显示名称可能不同于文件名。

- 若要将组的所有规则添加到自定义规则集，请选中组的复选框。 若要删除组中的所有规则，请清除该复选框。

- 若要向自定义规则集添加特定规则，请选中该规则的复选框。 若要从规则集中删除规则，请清除该复选框。

- 若要更改在代码分析中违反规则时采取的操作，请单击该规则的 "**操作**" 字段，然后选择以下值之一：

     **警告**-生成警告。

     **错误**-生成错误。

     **无**-禁用规则。 此操作与从规则集中删除规则的操作相同。

## <a name="changing-the-rule-set-editor-display"></a>更改规则集编辑器显示

#### <a name="to-group-filter-or-change-the-fields-in-the-rule-set-editor-by-using-the-rule-set-editor-toolbar"></a>使用规则集编辑器工具栏对规则集编辑器中的字段进行分组、筛选或更改

- 若要展开所有组中的规则，请单击 "**全部展开**"。

- 若要折叠所有组中的规则，请单击 "**全部折叠**"。

- 若要更改对规则进行分组所依据的字段，请从 "**分组依据**" 列表中选择字段。 若要显示未分组的规则，请选择 **\<None >** 。

- 若要在规则列中添加或删除字段，请单击**列选项**。

- 若要隐藏不适用于当前解决方案的规则，请**隐藏不适用于当前解决方案的规则**。

- 若要切换显示和隐藏分配了 "错误" 操作的规则，请单击 "**显示可以生成代码分析错误的规则**"。

- 若要切换显示和隐藏分配了 "警告" 操作的规则，请单击 "**显示可以生成代码分析警告的规则**"。

- 若要切换显示和隐藏分配了 "**无**" 操作的规则，请单击 "**显示未启用的规则**"。

- 若要添加或删除当前规则集的 Microsoft 默认规则集，请单击 "**添加或删除子规则集**"。

## <a name="see-also"></a>请参阅
 [如何：配置托管代码的代码分析项目](../code-quality/how-to-configure-code-analysis-for-a-managed-code-project.md)[代码分析规则集引用](../code-quality/code-analysis-rule-set-reference.md)
