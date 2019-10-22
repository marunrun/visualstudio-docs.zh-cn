---
title: 如何：更改调试单步执行选项（旧版） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- branch stepping
- debugging, stepping options
- debugging workflows, stepping options
- stepping, changing options
- instance stepping
ms.assetid: aedc06af-d58a-44d6-aee4-f397f1f923a0
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 5126b3dc45d33471080ae154e06f4a327e21fef7
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72663437"
---
# <a name="how-to-change-the-debug-stepping-option-legacy"></a>如何：更改调试单步执行选项（旧版）
本主题介绍如何在旧 [!INCLUDE[wf](../includes/wf-md.md)] 中，针对具有并发操作的 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 应用程序更改调试单步执行选项。 在需要面向 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 或 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 时，请使用旧 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]。

 调试具有并发执行的旧活动（如**ParallelActivity**或**ConditionedActivityGroup**）时，可以使用以下两个选项之一来单步执行代码。

 按照这些步骤在旧工作流项目中更改调试单步执行选项。

## <a name="procedures"></a>过程

#### <a name="to-change-the-debug-stepping-option"></a>更改调试单步执行选项

1. 启动 Visual Studio。

2. 打开现有的旧工作流项目，或创建使用并发活动并且面向 [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] 或 [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)] 的新项目。

3. 在旧版 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 中的 "**工作流**" 菜单上，指向 "**调试**"，然后指向 "**单步执行选项**"。

4. 选择 "**实例**" 或 "**分支**"。

## <a name="see-also"></a>请参阅
 [调试旧版工作流](../workflow-designer/debugging-legacy-workflows.md)[调试单步执行选项（旧版）](../workflow-designer/debug-stepping-options-legacy.md)