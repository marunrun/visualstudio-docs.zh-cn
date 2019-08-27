---
title: 如何：通过自定义滚动条来跟踪代码 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: a9ebe7ec-4b6f-4ba2-a79e-80fab3db485b
caps.latest.revision: 6
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: da6745b3980b6ef5b0200c91d4abf245daadfa71
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68186232"
---
# <a name="how-to-track-your-code-by-customizing-the-scrollbar"></a>如何：通过自定义滚动条来跟踪代码
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用长码文件时，可能很难记住所有内容。 可自定义代码窗口的滚动条，以便获得代码中所发生情况的鸟瞰图。  
  
### <a name="to-show-annotations-on-the-scroll-bar"></a>显示滚动条上的注释  
  
1. 可设置滚动条，以显示代码更改、断点、错误和书签。  
  
     打开**滚动条**选项页（**工具”，“选项文本编辑器”，“所有语言”或特定语言，或在快速启动窗口中键入“滚动条”）**  。  
  
2. 选择“在垂直滚动条上方显示注释”，然后选择要查看的注释  。 （“标记”选项包括断点和书签。）   
  
3. 现在试一试。打开大型代码文件，并替换出现在文件中多个位置的内容。 滚动条将显示替换的效果，从而在替换了不应替换的内容时可撤回更改。  
  
     下面是搜索字符串后滚动条的外观。 注意将显示字符串的所有实例。  
  
     ![搜索字符串后的滚动条](../ide/media/enhancedscrollbarsearch.png "EnhancedScrollbarSearch")  
  
     下面是替换字符串的所有实例后滚动条的外观。 将立即看到操作导致了一些问题。  
  
     ![替换字符串并发生错误后的滚动条](../ide/media/enhancedscrollbarreplace.png "EnhancedScrollbarReplace")  
  
### <a name="to-set-the-display-mode-for-the-scroll-bar"></a>设置滚动条的显示模式  
  
1. 滚动条具有两种模式：条状模式（默认）和映射模式。 条状模式只显示滚动条上的注释指示器。 映射模式下，在滚动条上表示代码行。 可选择它们的宽度，以及将指针停留在它们上时是否显示基础代码。 单击滚动条上的某个位置时，游标将移到代码中的该位置。 折叠区域所带的阴影不同；双击这些区域可将其展开。  
  
     在“滚动条”选项页上，选择“使用垂直滚动条的条状模式”或“使用垂直滚动条的映射模式”    。 可在“源概述”下拉列表中选择宽度  。  
  
     下面是启用映射模式且宽度设置为“中等”时搜索示例的外观：  
  
     ![映射模式中的滚动条](../ide/media/enhancedscrollbar.png "EnhancedScrollbar")  
  
2. 映射模式下，若要在滚动条上上下移动游标时启用代码预览，选择“显示预览工具提示”选项  。 下面是它的外观：  
  
     ![包含工具提示的滚动条](../ide/media/enhancedscrollbarsearchtooltip.png "EnhancedScrollbarSearchTooltip")  
  
     如果要保留映射模式滚动行为和预览工具提示，但不需要看到源代码概述，可将“源概述”设置为“关闭”   。
