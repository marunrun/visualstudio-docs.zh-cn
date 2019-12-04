---
title: 如何：配置性能规则 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.ruleseditor
ms.assetid: a148b468-b849-4858-880a-808a6b47e596
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: c9bb9b07a0ae1fa19ae48408aa34a9dfb6577b6e
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74779007"
---
# <a name="how-to-configure-performance-rules"></a>如何：配置性能规则
Visual Studio 分析工具的性能警告指示所分析应用程序中可能会减慢程序执行的问题。 警告还可指示可能需要更改收集方法才能收集更多有用的数据。 系统会在分析会话中自动生成性能警告，并且在 [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] 中打开分析数据文件时，警告将显示在**错误列表**窗口中。 某些警告可能不适用于你感兴趣的某些方案，而某些警告则可能属于误报。 可以配置性能警告以显示或隐藏特定的警告。

### <a name="to-configure-profiler-performance-warnings"></a>配置事件探查器性能警告

1. 在 **“工具”** 菜单上，单击 **“选项”** 。

2. 展开“性能工具”  ，然后单击“规则”  。

3. 若要启用或禁用某个警告，请选择或清除该警告 **ID** 和名称旁边的复选框。

4. 若要指定规则的警告级别，请单击规则旁边的“操作”  单元格，然后单击警告等级。

    - **已禁用** - 禁用规则（等同于清除规则 ID 旁边的复选框）。

    - **警告** - 将规则显示为警告。

    - **错误** - 停止分析执行并将规则显示为错误。

    - **信息** - 仅将规则显示为信息。
