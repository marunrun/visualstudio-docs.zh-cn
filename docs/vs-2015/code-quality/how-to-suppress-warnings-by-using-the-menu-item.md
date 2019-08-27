---
title: 如何：使用菜单项禁止显示警告 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
helpviewer_keywords:
- warnings, suppressing
- code analysis, suppressing warnings
ms.assetid: 36bd1850-dcde-4ed0-9bc3-0b83df434362
caps.latest.revision: 26
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 5097ecb0f7458e739def275d616eb344a2a6db0d
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63426566"
---
# <a name="how-to-suppress-warnings-by-using-the-menu-item"></a>如何：使用菜单项禁止显示警告
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

备注
> 在源代码中，不支持对网站项目进行禁止显示操作。  
  
 你可以使用“代码分析”窗口来禁止显示代码分析警告。 禁止显示警告与禁用不同。 禁止显示警告时，它仅适用于此违反行为的特定实例。 仍将在错误列表窗口中报告相同的警告的其他冲突。  
  
 在运行代码分析之后，你可能会确定“代码分析”窗口中显示的一条或多条代码分析警告不适用于你的应用程序。 例如，您可能确定代码正确，因为是。 或者，它可能会出现这种情况，某些冲突优先级较低，将不在当前的开发周期中修复。 无论是什么原因，指出不适用的警告经常会很有帮助，这样，小组成员就会知道已检查过代码并且已确定可禁止显示该警告。 在源代码中，禁止显示功能很有用，因为它可以让您将禁止显示功能放在生成警告的位置附近。  
  
 您可以选择禁止显示是否将出现在源代码中或全局禁止显示文件中。 必须在全局禁止显示文件中放置一些禁止显示。 如果出现这种情况，**在源**选项将被禁用。  
  
### <a name="to-suppress-a-warning-by-using-menu-item"></a>若要使用菜单项禁止显示警告  
  
1. 上**分析**菜单中，选择**Windows** ，然后选择**代码分析**。  
  
2. 在中**代码分析**窗口中，选择警告禁止显示。  
  
3. 选择操作，然后选择**禁止显示消息**，然后选择**在源**或**在项目禁止显示文件**。  
  
     特定警告将被禁止显示，并且带着删除线显示在“代码分析”窗口中。  
  
> [!NOTE]
> 不具有目标的禁止显示出现在全局禁止显示文件。
