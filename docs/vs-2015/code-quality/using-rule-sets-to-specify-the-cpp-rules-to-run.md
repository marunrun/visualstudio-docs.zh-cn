---
title: 使用规则集指定要运行的 c + + 规则 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
ms.assetid: ac3877e6-5349-4c03-9541-3d5be259f1e8
caps.latest.revision: 7
author: corob-msft
ms.author: corob
manager: jillfra
ms.openlocfilehash: ff105af1d817613b324e1158130457eb906c753f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "77277862"
---
# <a name="using-rule-sets-to-specify-the-c-rules-to-run"></a>使用规则集指定要运行的 C++ 规则
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 [!INCLUDE[vsPreShort](../includes/vspreshort-md.md)] 和中 [!INCLUDE[vsUltShort](../includes/vsultshort-md.md)] ，你可以创建和修改自定义 *规则集* ，以满足与代码分析相关的特定项目需求。 若要创建自定义 C++ 规则集，必须在 Visual Studio IDE 中打开 C/C++ 项目。 然后，在规则集编辑器中打开某一标准规则集，再添加或移除特定的规则，并且可更改当代码分析确定违反规则时所发生的操作。  
  
 若要创建新的自定义规则集，请使用新文件名进行保存。 自定义规则集会自动分配给项目。  
  
## <a name="opening-the-rule-set-editor"></a>打开规则集编辑器  
  
#### <a name="to-create-a-custom-rule-from-a-single-existing-rule-set"></a>基于单个现有规则集创建自定义规则  
  
1. 在解决方案资源管理器中，打开项目的快捷菜单，然后选择 " **属性**"。  
  
2. 在 " **属性** " 选项卡上，选择 " **代码分析**"。  
  
3. 在 " **规则集** " 下拉列表中，执行下列操作之一：  
  
   - 选择要自定义的规则集。  
  
     \- 或 -  
  
   - 选择 **\<Browse...>** 指定列表中不存在的现有规则集。  
  
4. 选择 " **打开** " 以在规则集编辑器中显示规则。  
  
#### <a name="to-modify-a-rule-set-in-the-rule-set-editor"></a>在规则集编辑器中修改规则集  
  
- 若要更改规则集的显示名称，请在 " **视图** " 菜单上选择 " **属性窗口**"。 在 " **名称** " 框中输入显示名称。 请注意，显示名称可能不同于文件名。  
  
- 若要将组的所有规则添加到自定义规则集，请选中组的复选框。 若要删除组中的所有规则，请清除该复选框。  
  
- 若要向自定义规则集添加特定规则，请选中该规则的复选框。 若要从规则集中删除规则，请清除该复选框。  
  
- 若要更改在代码分析中违反规则时采取的操作，请选择该规则的 " **操作** " 字段，然后选择以下值之一：  
  
     **警告** -生成警告。  
  
     **错误** -生成错误。  
  
     **无** -禁用规则。 此操作与从规则集中删除规则的操作相同。  
  
#### <a name="to-group-filter-or-change-the-fields-in-the-rule-set-editor-by-using-the-rule-set-editor-toolbar"></a>使用规则集编辑器工具栏对规则集编辑器中的字段进行分组、筛选或更改  
  
- 若要展开所有组中的规则，请选择 " **全部展开**"。  
  
- 若要折叠所有组中的规则，请选择 " **全部折叠**"。  
  
- 若要更改对规则进行分组所依据的字段，请从 " **分组依据** " 列表中选择字段。 若要显示未分组的规则，请选择 **\<None>** 。  
  
- 若要在规则列中添加或删除字段，请选择 **列选项**。  
  
- 若要隐藏不适用于当前解决方案的规则，请选择 " **隐藏不适用于当前解决方案的规则**"。  
  
- 若要切换显示和隐藏分配了 "错误" 操作的规则，请选择 " **显示可以生成代码分析错误的规则**"。  
  
- 若要切换显示和隐藏分配了 "警告" 操作的规则，请选择 " **显示可以生成代码分析警告的规则**"。  
  
- 若要切换显示和隐藏分配了 " **无** " 操作的规则，请选择 " **显示未启用的规则**"。  
  
- 若要添加或删除当前规则集的 Microsoft 默认规则集，请选择 " **添加或删除子规则集**"。
