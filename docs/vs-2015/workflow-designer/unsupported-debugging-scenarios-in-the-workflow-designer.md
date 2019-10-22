---
title: 工作流设计器中不支持的调试方案 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: 6adbe379-41d0-4681-9cd0-b91f187c3c2c
caps.latest.revision: 4
author: steved0x
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: fdbe68b416560b85580e3dd30e5f8138b7cd08fe
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72606940"
---
# <a name="unsupported-debugging-scenarios-in-the-workflow-designer"></a>工作流设计器中不受支持的调试方案
[!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)] 中的工作流设计器添加了许多新功能，但仍存在一些它不支持的调试方案。 本文档详细介绍了不受支持的工作流设计器调试方案。

- 在编辑代码之后不能继续执行。

- 不能从工作流中的任意点继续执行（“设置下一语句”）。

- 只有在到达光标处之后才能继续执行（“运行到光标处”）。

- 不能使用工作流设计器来调试通过代码创建（未使用工作流设计器）的工作流。

- 也不能在 [!INCLUDE[wf](../includes/wf-md.md)] 设计器中调试通过 [!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)] 早期版本创建的工作流。

- 不能在两个活动或 <xref:System.Activities.Statements.Flowchart> 节点之间的链接上定义断点。

- 调试期间剪贴板不可用。

- 复制或粘贴活动时不会保留断点。

- 不能在调用堆栈窗口中设置工作流断点。

- 在设计器中创建断点时，不使用 "**新建断点**" 对话框中的**行**和**字符**设置。

- “断点”窗口或快捷菜单不支持以下用于工作流调试的列或选项：

  - 条件

  - 命中次数

  - 命中条件

  - 函数

  - 数据

  - 过程

  - 转到反汇编
