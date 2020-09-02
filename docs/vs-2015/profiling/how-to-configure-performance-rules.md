---
title: 如何：配置性能规则 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.ruleseditor
ms.assetid: a148b468-b849-4858-880a-808a6b47e596
caps.latest.revision: 19
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 71593496613c75485fd30481777d0fcc1102c11c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68179587"
---
# <a name="how-to-configure-performance-rules"></a>如何：配置性能规则
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 分析工具的性能警告指示所分析应用程序中可能会减慢程序执行的问题。 警告还可指示可能需要更改收集方法才能收集更多有用的数据。 系统会在分析会话中自动生成性能警告，并且在 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 中打开分析数据文件时，警告将显示在**错误列表**窗口中。 某些警告可能不适用于你感兴趣的某些方案，而某些警告则可能属于误报。 可以配置性能警告以显示或隐藏特定的警告。  
  
### <a name="to-configure-profiler-performance-warnings"></a>配置事件探查器性能警告  
  
1. 在 **“工具”** 菜单上，单击 **“选项”** 。  
  
2. 展开“性能工具”，然后单击“规则”。  
  
3. 若要启用或禁用某个警告，请选择或清除该警告 **ID** 和名称旁边的复选框。  
  
4. 若要指定规则的警告级别，请单击规则旁边的“操作”单元格，然后单击警告等级。  
  
    - **已禁用** - 禁用规则（等同于清除规则 ID 旁边的复选框）。  
  
    - **警告** - 将规则显示为警告。  
  
    - **错误** - 停止分析执行并将规则显示为错误。  
  
    - **信息** - 仅将规则显示为信息。
