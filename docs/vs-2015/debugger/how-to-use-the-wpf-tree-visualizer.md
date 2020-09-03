---
title: 如何：使用 WPF 树可视化工具 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- WPF, debugging
- debugging, WPF
ms.assetid: 2a1bf1cd-90f9-4d06-9fb4-1bfc925afef3
caps.latest.revision: 21
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 381dc45351ae03e615afbdd31239869e3dba8e4e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "67825439"
---
# <a name="how-to-use-the-wpf-tree-visualizer"></a>如何：使用 WPF 树可视化工具
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以使用 WPF 树可视化工具浏览 WPF 对象的可视化树，并查看该树中所含对象的 WPF 依赖项属性。 有关可视化树的详细信息，请参阅 [WPF 中的树](https://msdn.microsoft.com/library/e83f25e5-d66b-4fc7-92d2-50130c9a6649)。 有关依赖项属性的详细信息，请参阅[依赖项属性概述](https://msdn.microsoft.com/library/d119d00c-3afb-48d6-87a0-c4da4f83dee5)。  
  
 当你打开 WPF 树可视化工具后，将看到以下两个窗格：位于左侧的“可视化树”窗格和位于右侧的“Name:Type 属性”窗格 。 选择“可视化树”窗格中的任意对象，“Name:Type 属性”窗格会自动更新为显示该对象的属性 。  
  
### <a name="to-open-the-wpf-tree-visualizer"></a>打开 WPF 树可视化工具  
  
1. 在数据提示、“监视”窗口、“自动”窗口或“局部变量”窗口中，在 WPF 对象名称旁单击放大镜图标旁的箭头  。  
  
     将会显示可视化工具列表。  
  
2. 单击“WPF 树可视化工具”。  
  
### <a name="to-search-the-visual-tree"></a>搜索可视化树  
  
- 在“可视化树”窗格中，在“搜索”框中键入要搜索的字符串 。  
  
  WPF 树可视化工具将立即在可视化树中查找与您键入的字符串匹配的第一个对象。 键入更多字符可找到更精确的匹配项。  

  - 若要转到可视化树中的下一个匹配项，请单击“下一个”。  

  - 若要返回上一个匹配项，请单击“上一个”。  

  - 若要清除搜索条件，请单击“清除”。  

### <a name="to-search-the-properties-list"></a>搜索属性列表  
  
- 在 " **Properties of** _名称_**：**_类型_" 窗格的 "属性" 中，在 "**筛选器**" 框中键入要搜索的字符串。  
  
  WPF 树可视化工具将立即查找与你键入的字符串匹配的属性；现在，列表中仅显示与键入的字符串匹配的那些属性。 键入更多字符可找到更精确的匹配项。  

  - 若要清除搜索条件，请单击“清除”。  
  
### <a name="to-close-the-visualizer"></a>关闭可视化工具  
  
- 单击对话框右上角的“关闭”图标。  
  
## <a name="see-also"></a>另请参阅  
 [如何：使用可视化工具](../misc/how-to-use-a-visualizer.md)   
 [创建自定义可视化工具](../debugger/create-custom-visualizers-of-data.md)   
 [WPF 中的树](https://msdn.microsoft.com/library/e83f25e5-d66b-4fc7-92d2-50130c9a6649)   
 [依赖项属性概述](https://msdn.microsoft.com/library/d119d00c-3afb-48d6-87a0-c4da4f83dee5)
