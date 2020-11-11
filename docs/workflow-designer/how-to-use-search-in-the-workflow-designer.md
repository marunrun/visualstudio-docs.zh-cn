---
title: 如何：在工作流设计器中使用搜索
description: 了解如何在工作流设计器中搜索以按关键字查找项，以便你可以轻松创建更大、更复杂的工作流。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: f42d3115-2ed2-4941-8f1e-92dac41c30fa
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3dadaf6ce4728dfac8d4052804cbed70ee7cefcd
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2020
ms.locfileid: "94437900"
---
# <a name="how-to-use-search-in-the-workflow-designer"></a>如何：在工作流设计器中使用搜索

为了便于创建更大、更复杂的工作流，你可以在工作流设计器中搜索以按关键字查找项。 请注意，设计器不支持替换。

## <a name="quick-find"></a>快速查找

"快速查找" 在设计器中查找以下内容：

- <xref:System.Activities.Activity> 对象、<xref:System.Activities.Statements.FlowNode> 对象、<xref:System.Activities.Statements.State> 对象、转换以及其他自定义流控制项的属性。

- 变量

- 参数

- 表达式

### <a name="use-quick-find"></a>使用快速查找

1. 打开工作流设计器后，按 **Ctrl + F** ，或选择 " **编辑**  >  **查找并替换**  >  **快速查找** "。

2. 在 " **查找内容** " 文本框中输入搜索词，然后单击 " **查找下一个** "。

3. 搜索词位于当前工作流中。 下图显示了位于设计器中的活动显示名称：

   ![在工作流设计器中搜索结果](../workflow-designer/media/designersearch.png)

## <a name="find-in-files"></a>在文件中查找

"在文件中查找" 在工作流文件（包括 XAML 文件）中查找字符串。

### <a name="use-find-in-files"></a>使用 "在文件中查找"

1. 在 Visual Studio 中，按 **Ctrl** + **Shift** + **F** ，或选择 " **编辑**  >  **查找并替换**  >  **在文件中查找** "。

2. 在 " **查找内容** " 文本框中输入搜索项，并单击 " **查找所有** 内容"。

3. 查找结果将显示在 " **查找结果** " 视图中。 双击某一结果项会在工作流设计器中导航到包含匹配项的活动。