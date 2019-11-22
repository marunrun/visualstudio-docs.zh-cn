---
title: 'How to: Create a PolicyActivity Rule Set (Legacy) | Microsoft Docs'
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

 After you have dragged a **Policy** activity item from the **Toolbox** to the workflow design surface, you will want to select an existing rule or create a new rule set for the [PolicyActivity](https://go.microsoft.com/fwlink?LinkID=65019) activity. You select an existing rule set by using the [Select Rule Set Dialog Box (Legacy)](../workflow-designer/select-rule-set-dialog-box-legacy.md) and you create rule sets by using the [Rule Set Editor Dialog Box (Legacy)](../workflow-designer/rule-set-editor-dialog-box-legacy.md).

> [!NOTE]
> You can open the [Rule Set Editor Dialog Box (Legacy)](../workflow-designer/rule-set-editor-dialog-box-legacy.md) dialog box directly by double-clicking on a [PolicyActivity](https://go.microsoft.com/fwlink?LinkID=65019) activity that is on the workflow design surface.

### <a name="to-select-or-create-a-rule-set-for-a-policyactivity-activity"></a>为 PolicyActivity 活动选择或创建规则集

1. Right-click the [PolicyActivity](https://go.microsoft.com/fwlink?LinkID=65019), and then click **Properties** to open the **Properties** window.

2. Click the **RuleSetReference** property.

3. 执行以下操作之一：

    - Click the **RuleSetReference** ellipses **[…]** , and then select an existing rule set in the [Select Rule Set Dialog Box (Legacy)](../workflow-designer/select-rule-set-dialog-box-legacy.md). 然后转到步骤 10。

         或

    - 键入规则集的名称。 Click the **RuleSetReference** ellipses **[…]** , and then select **Edit** in the [Select Rule Set Dialog Box (Legacy)](../workflow-designer/select-rule-set-dialog-box-legacy.md).

         或

    - 键入规则集的名称。 Expand the **RuleSetReference** property and select the ellipses **[…]** in the **RuleSet Definition** property.

         The [Rule Set Editor Dialog Box (Legacy)](../workflow-designer/rule-set-editor-dialog-box-legacy.md) opens.

4. In the [Rule Set Editor Dialog Box (Legacy)](../workflow-designer/rule-set-editor-dialog-box-legacy.md), click **Add Rule** to add a new rule to the rule set.

5. Enter the **Name**, **Priority**, and **Reevaluation** properties, or keep the default values.

6. Enter the text for the **Condition**.

7. Enter the text for the **Then Actions** and the **Else Actions**.

8. Click **Add Rule** again to add another rule.

9. 完成后单击“确定”。

## <a name="see-also"></a>请参阅
 [PolicyActivity](https://go.microsoft.com/fwlink?LinkID=65019) [Select Rule Set Dialog Box (Legacy)](../workflow-designer/select-rule-set-dialog-box-legacy.md) [Rule Set Editor Dialog Box (Legacy)](../workflow-designer/rule-set-editor-dialog-box-legacy.md) [Using the Policy Activity](https://go.microsoft.com/fwlink?LinkID=65004) [Legacy Workflow Activities](../workflow-designer/legacy-workflow-activities.md)