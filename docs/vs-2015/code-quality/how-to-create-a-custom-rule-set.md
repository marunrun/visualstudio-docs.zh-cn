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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 909242aaf8dd4caaee7af75e40554aaff648df68
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68201369"
---
# <a name="how-to-create-a-custom-rule-set"></a>如何：创建自定义规则集
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在中[!INCLUDE[vsUltShort](../includes/vsultshort-md.md)]， [!INCLUDE[vsPreShort](../includes/vspreshort-md.md)]，并[!INCLUDE[vsPro](../includes/vspro-md.md)]，可以创建和修改自定义*规则集*以满足与代码分析相关联的特定项目需求。 若要创建自定义规则集，在打开一个或多个标准规则设置规则集编辑器中。 然后可以添加或移除特定的规则，可以更改当代码分析确定违反了一个规则时发生的操作。  
  
 若要创建新的自定义规则集，通过使用新的文件名保存。 自定义规则集自动分配给项目。  
  
## <a name="opening-the-rule-set-editor"></a>打开规则集编辑器  
  
#### <a name="to-open-an-empty-rule-set-file-in-the-rule-set-editor"></a>若要打开一个空规则文件中设置规则集编辑器  
  
1. 上**文件**菜单[!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]，依次指向**新建**，然后单击**文件**。  
  
2. 在中**新的文件**对话框中，单击**常规**中**已安装的模板**列表，然后再选择**代码分析规则集**。  
  
3. 规则集编辑器随即出现。 在编辑器的列表中不选择任何规则。  
  
#### <a name="to-create-a-custom-rule-from-a-single-existing-rule-set"></a>若要从单个的现有规则集创建自定义规则  
  
1. 在解决方案资源管理器，右键单击项目，然后选择**属性**。  
  
2. 上**属性**选项卡上，单击**代码分析**。  
  
3. 在中**规则集**下拉列表中，执行下列任一操作：  
  
   - 选择想要自定义的规则集。  
  
     \- 或 -  
  
   - 选择 **\<浏览...>** 指定的现有规则集不在列表中。  
  
4. 单击**打开**若要在规则集编辑器中显示的规则。  
  
#### <a name="to-create-a-custom-rule-set-from-multiple-existing-rule-sets"></a>若要创建自定义规则集从多个现有规则集  
  
1. 在解决方案资源管理器，右键单击项目，然后选择**属性**。  
  
2. 上**属性**选项卡上，单击**代码分析**。  
  
3. 选择 **\<选择多个规则集...>** 从 **运行此规则集** 。  
  
4. 在中**添加或删除规则集**对话框中，选择规则集想要基于新的规则集，然后单击**确定**。  
  
5. 保存新的规则集。  
  
     在中选择新的规则集的名称**运行此规则集**列表。 可以更改下一步中的规则集的显示名称。  
  
6. （可选）若要更改在规则集的显示名称**视图**菜单上，单击**属性窗口**。 键入中的显示名称**名称**框。  
  
7. 若要添加，删除，或修改新规则集中的特定代码分析规则，请单击**打开**。  
  
## <a name="modifying-a-rule-set"></a>修改规则集  
  
#### <a name="to-modify-a-rule-set-in-the-rule-set-editor"></a>若要修改的规则将设置规则集编辑器  
  
- 若要更改在规则集的显示名称**视图**菜单上，单击**属性窗口**。 输入中的显示名称**名称**框。 请注意，显示名称可能不同于文件名称。  
  
- 若要添加到自定义规则集的组的所有规则，请选择组的复选框。 若要删除的组的所有规则，请清除该复选框。  
  
- 若要将特定的规则添加到自定义规则集，请选择规则的复选框。 若要从规则集中删除规则，请清除该复选框。  
  
- 若要更改的代码分析中违反规则时执行的操作，请单击**操作**字段规则，然后选择以下值之一：  
  
     **则发出警告**-生成警告。  
  
     **错误**-将生成错误。  
  
     **无**-禁用规则。 此操作是从规则集内移除规则相同的。  
  
## <a name="changing-the-rule-set-editor-display"></a>更改规则集编辑器的显示  
  
#### <a name="to-group-filter-or-change-the-fields-in-the-rule-set-editor-by-using-the-rule-set-editor-toolbar"></a>要进行分组，筛选，或者通过使用规则集编辑器工具栏来更改规则集编辑器中的字段  
  
- 若要展开所有组中的规则，请单击**全部展开**。  
  
- 若要折叠所有组中的规则，请单击**折叠所有**。  
  
- 若要更改规则分组所依据的字段，选择从字段**Group By**列表。 若要显示未分组的规则，请选择 **\<None >** 。  
  
- 若要添加或删除字段，在规则列中，单击**列选项**。  
  
- 若要隐藏不适用于当前解决方案中，规则**隐藏不适用于当前解决方案的规则**。  
  
- 若要切换显示和隐藏分配了错误操作的规则，请单击**显示可以生成代码分析错误的规则**。  
  
- 若要切换显示和隐藏分配了警告操作规则，请单击**显示可以生成代码分析警告的规则**。  
  
- 若要切换显示和隐藏分配了规则**无**操作中，单击**显示未启用的规则**。  
  
- 若要添加或移除的 Microsoft 默认规则设置为当前的规则集，请单击**添加或移除子规则集**。  
  
## <a name="see-also"></a>请参阅  
 [如何：配置托管的代码项目的代码分析](../code-quality/how-to-configure-code-analysis-for-a-managed-code-project.md)   
 [代码分析规则集参考](../code-quality/code-analysis-rule-set-reference.md)
