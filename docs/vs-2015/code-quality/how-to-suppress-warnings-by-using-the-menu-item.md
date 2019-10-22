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
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 96b7433ff4f696989142aa2c2ce47982006b93b2
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72610017"
---
# <a name="how-to-suppress-warnings-by-using-the-menu-item"></a>如何：使用菜单项禁止显示警告
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

备注
> 在源代码中，不支持对网站项目进行禁止显示操作。

 你可以使用“代码分析”窗口来禁止显示代码分析警告。 禁止显示警告与禁用不同。 当你禁止显示警告时，它仅适用于特定的冲突实例。 同一警告的其他冲突仍将在 "错误列表" 窗口中报告。

 在运行代码分析之后，你可能会确定“代码分析”窗口中显示的一条或多条代码分析警告不适用于你的应用程序。 例如，你可能会确定代码是正确的。 或者，可能是某些冲突的优先级较低，并且在当前开发周期中不会修复。 无论是什么原因，指出不适用的警告经常会很有帮助，这样，小组成员就会知道已检查过代码并且已确定可禁止显示该警告。 在源代码中，禁止显示功能很有用，因为它可以让您将禁止显示功能放在生成警告的位置附近。

 您可以选择禁止显示出现在源代码中还是出现在全局禁止显示文件中。 某些禁止显示必须放置在全局禁止显示文件中。 如果是这种情况，则会禁用 "**在源中**" 选项。

### <a name="to-suppress-a-warning-by-using-menu-item"></a>使用菜单项禁止显示警告

1. 在 "**分析**" 菜单上，选择 "**窗口**"，然后选择 "**代码分析**"。

2. 在 "**代码分析**" 窗口中，选择警告抑制。

3. 选择 "操作"，然后选择 "**禁止显示消息**"，然后**在 "源**" 或 **"在项目禁止显示文件**" 中选择。

     特定警告将被禁止显示，并且带着删除线显示在“代码分析”窗口中。

> [!NOTE]
> 没有目标的禁止显示出现在全局禁止显示文件中。
