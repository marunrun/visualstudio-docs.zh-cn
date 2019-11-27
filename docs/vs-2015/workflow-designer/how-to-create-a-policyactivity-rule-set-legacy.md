---
title: 如何：创建 PolicyActivity 规则集（旧版） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- PolicyActivity activity, creating rule sets
- Rule Set Editor dialog box
- PolicyActivity activity, selecting rule sets
- Select Rule Set dialog box
- rule sets, creating for PolicyActivity
ms.assetid: f272489d-3342-4511-8b59-6a0fd7a42d70
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 1c18a08986bf8e4aa30969a9d30d740fb68e978c
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297478"
---
# <a name="how-to-create-a-policyactivity-rule-set-legacy"></a>如何：创建 PolicyActivity 规则集（旧版）
本主题介绍如何使用面向 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 或 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 的旧 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)] 来创建策略活动规则集。

 将 "**策略**" 活动项从 "**工具箱**" 拖动到工作流设计图面之后，您将需要为[PolicyActivity](https://go.microsoft.com/fwlink?LinkID=65019)活动选择现有规则或创建新规则集。 使用 "[选择规则集" 对话框（旧版）](../workflow-designer/select-rule-set-dialog-box-legacy.md)选择现有规则集，并使用 "[规则集编辑器" 对话框（旧版）](../workflow-designer/rule-set-editor-dialog-box-legacy.md)创建规则集。

> [!NOTE]
> 通过双击工作流设计图面上的[PolicyActivity](https://go.microsoft.com/fwlink?LinkID=65019)活动，可以直接打开 "[规则集编辑器" 对话框（旧版）](../workflow-designer/rule-set-editor-dialog-box-legacy.md)对话框。

### <a name="to-select-or-create-a-rule-set-for-a-policyactivity-activity"></a>为 PolicyActivity 活动选择或创建规则集

1. 右键单击[PolicyActivity](https://go.microsoft.com/fwlink?LinkID=65019)，然后单击 "**属性**" 以打开 "**属性**" 窗口。

2. 单击 " **RuleSetReference** " 属性。

3. 执行下列操作之一：

    - 单击 " **RuleSetReference** " 省略号 " **[...]** "，然后在 "[选择规则集" 对话框（旧版）](../workflow-designer/select-rule-set-dialog-box-legacy.md)中选择现有规则集。 然后转到步骤 10。

         或

    - 键入规则集的名称。 单击 " **RuleSetReference** " 省略号 " **[...]** "，然后在 "[选择规则集" 对话框（旧版）](../workflow-designer/select-rule-set-dialog-box-legacy.md)中选择 "**编辑**"。

         或

    - 键入规则集的名称。 展开 " **RuleSetReference** " 属性，然后选择 "**规则集定义**" 属性中的省略号 **[...]** 。

         "[规则集编辑器" 对话框（旧版）](../workflow-designer/rule-set-editor-dialog-box-legacy.md)将打开。

4. 在 "[规则集编辑器" 对话框（旧版）](../workflow-designer/rule-set-editor-dialog-box-legacy.md)中，单击 "**添加规则**" 将新规则添加到规则集。

5. 输入 "**名称**"、"**优先级**" 和 "**重估**" 属性，或保留默认值。

6. 输入**条件**的文本。

7. 输入**Then 操作**和**Else 操作**的文本。

8. 再次单击 "**添加规则**"，添加另一个规则。

9. 完成后单击“确定”。

## <a name="see-also"></a>请参阅
 " [PolicyActivity](https://go.microsoft.com/fwlink?LinkID=65019) [选择规则集](../workflow-designer/select-rule-set-dialog-box-legacy.md)" 对话框（旧版） "[规则集编辑器" 对话框（旧版）](../workflow-designer/rule-set-editor-dialog-box-legacy.md) [使用策略活动](https://go.microsoft.com/fwlink?LinkID=65004)[旧版工作流活动](../workflow-designer/legacy-workflow-activities.md)