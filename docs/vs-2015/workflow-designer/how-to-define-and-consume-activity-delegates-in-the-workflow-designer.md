---
title: 如何：在工作流设计器中定义和使用活动委托 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: c68e42ad-3ec0-4c2d-b104-fe36c6d83b5e
caps.latest.revision: 3
author: steved0x
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 26ba92a2ba7aa6eed471383c875104549e896804
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72603858"
---
# <a name="how-to-define-and-consume-activity-delegates-in-the-workflow-designer"></a>如何：在工作流设计器中定义和使用活动委托
[!INCLUDE[net_v45](../includes/net-v45-md.md)] 包括 <xref:System.Activities.Statements.InvokeDelegate> 活动的新的现成设计器。 此设计器可用于将委托分配给从 <xref:System.Activities.ActivityDelegate> 派生的活动，例如 <xref:System.Activities.ActivityAction> 或 <xref:System.Activities.ActivityFunc%601>。

### <a name="define-an-activity-delegate"></a>定义活动委托

1. 在 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]中，选择 "**文件**"、"**新建**"、"**项目**"。 选择左侧的 "**工作流**" 节点，并在右侧选择 "**工作流控制台应用程序**" 模板。 为项目命名（如果需要），然后单击 **"确定"** 。

2. 在**解决方案资源管理器**中右键单击该项目，然后选择 "**添加**"、"**新建项 ...** "。 选择左侧的 "**工作流**" 节点，并在右侧选择**活动**模板。 将新活动命名为**MyForEach** ，然后单击 **"确定"** 。 将在工作流设计器中打开活动。

3. 在工作流设计器中，单击 "**参数**" 选项卡。

4. 单击 **“创建参数”** 。 将新参数命名为**Items**。

5. 在 "**参数类型**" 列中，选择 " **[T] 的数组**"。

6. 在类型浏览器中，选择 "**对象**"。 单击 **“确定”** 。

7. 再次单击 "**创建参数**"。 命名新的参数**体**。 在新参数的 "**方向**" 列中，选择 "**属性**"。

8. 在 "参数类型" 列中，选择 "**浏览类型 ...** "

9. 在类型浏览器的 "**类型名称**" 字段中，输入**ActivityAction** 。 选择树视图中的 " **ActivityAction\<t" >** 。 选择下拉列表中的 "**对象**"，将类型**ActivityAction\<对象 >** 分配给参数。

10. 将 "<xref:System.Activities.Statements.While>" 活动从 "工具箱" 的 "**控制流**" 部分拖到设计器图面。

11. 选择 "<xref:System.Activities.Statements.While>" 活动，然后选择 "**变量**" 选项卡。

12. 选择 "**创建变量**"。 命名新的变量**索引**。

13. 在 "**变量类型**" 列中，选择 " **Int32**"。 将**范围**保持为**While**，并将**默认**列留空。

14. 将 "<xref:System.Activities.Statements.While>" 活动的 " **Condition** " 属性设置为 "**索引 < 项**"。

15. 将 "<xref:System.Activities.Statements.InvokeDelegate>" 活动从 "工具箱" 的 "**基元**" 部分拖到 "<xref:System.Activities.Statements.While>" 活动的 "**正文**"。

16. 选择委托下拉的 "**正文**"。

17. 在 <xref:System.Activities.Statements.InvokeDelegate> 活动的 "**属性**" 网格中，单击 " **...** " 按钮。

18. 在 "参数命名**参数**" 的 "**值**" 列中，输入**Items [Index]** 。 单击 **"确定"** 以关闭 " **DelegateArguments** " 对话框。

19. 将 <xref:System.Activities.Statements.Assign> 活动拖到 <xref:System.Activities.Statements.InvokeDelegate> 活动的水平线下。 将创建 <xref:System.Activities.Statements.Assign> 活动，并将自动创建一个 <xref:System.Activities.Statements.Sequence> 活动，以包含**MyForEach**活动的 "**正文**" 部分中的两个活动。 需要序列，因为**正文**部分只能包含单个活动。 自动创建新的 <xref:System.Activities.Statements.Sequence> 活动是 [!INCLUDE[net_v45](../includes/net-v45-md.md)] 的一个新功能。

20. 将 <xref:System.Activities.Statements.Assign> 活动的 " **to** " 属性设置为 "**索引**"。 将 " **Assign** " 活动的 "**值**" 属性设置为 "**索引 + 1**"。

    自定义**MyForEach**活动现在将对通过**Items**集合传入它的每个值调用一次任意活动，并将集合中的值用作活动的输入。

### <a name="use-the-custom-activity-in-a-workflow"></a>使用工作流中的自定义活动

1. 按**Ctrl + Shift + B**生成项目。

2. 在**解决方案资源管理器**中，在设计器中打开**workflow1.xaml** 。

3. 将**MyForEach**活动从工具箱拖到设计器图面。 该活动将位于工具箱的某个部分中，其名称与项目名称相同。

4. 将**MyForEach**活动的**Items**属性设置为**new Object [] {1，"abc"}** 。

5. 将 <xref:System.Activities.Statements.WriteLine> 活动从工具箱的 "**基元**" 部分拖到 " **MyForEach** " 活动的 "**委托：正文**" 部分。

6. 将 <xref:System.Activities.Statements.WriteLine> 活动的**Text**属性设置为**Argument （）** 。

   当执行工作流时，控制台将显示以下信息：

   **1**
   **abc**