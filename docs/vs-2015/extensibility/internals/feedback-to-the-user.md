---
title: 向用户反馈 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- user model feedback
- environment, context
- IDE, context
- IDE, user feedback
ms.assetid: 2d472a24-3813-4f5f-9783-b491ad8a71ad
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7773c611733ccec525fc25264311e72c1dfe36e2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62537675"
---
# <a name="feedback-to-the-user"></a>为用户提供反馈
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

在[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]集成的开发环境 (IDE)，有关可用的功能基于用户的当前所选内容和全局选定内容上下文的可视反馈。 下表列出了在不同的选定内容上下文中可用的功能。  
  
|选定内容上下文|可用的功能|  
|-----------------------|-----------------------------|  
|IDE|Global|  
|当前产品设置|产品特定|  
|活动的层次结构|特定于类型的层次结构|  
|活动的层次结构项|特定于层次结构项类型|  
|活动文档|特定于文档类型|  
|最顶层的多文档界面 (MDI) 窗口|特定于窗口类型|  
|当前选定内容上下文|特定的选定内容上下文|  
  
 如果仅显示用户需要和持续提供一致的选择和环境上下文反馈的功能，则减少在 IDE 中的复杂性。 每次在 IDE 中打开一个窗口，将应用以下规则：  
  
- 如果窗口更改其选定内容上下文，在窗口中，明确地指示所选内容的反馈，并在动态帮助窗口中，如果所示，将更新以反映当前上下文。  
  
- 如果窗口更改全局选定内容上下文，所有特定于上下文菜单、 活动的层次结构窗口和应用程序标题栏将更新以反映当前上下文。  
  
- 在窗口应图面中的当前选定的属性**属性**窗口和 （可选） 所示，如果**属性页**对话框。  
  
- 它不再是活动窗口在 IDE 中时，如果窗口不显示属性或更改全局选定内容上下文，所选内容的反馈应不会保留在该窗口中。  
  
- 所有特定于文档的工具窗口应不断地反映活动文档。  
  
- 菜单、 工具栏和应用程序标题栏应反映最顶层的多文档界面 (MDI) 客户端窗口。  
  
  例如，当打开 Web 窗体中的 Visual Basic Web 应用程序项目的 HTML 视图，且用户选择`<td>`标记，按以下方式提供反馈：  
  
- 指示在活动窗口中，反映在所选内容**属性**窗口。  
  
- 特定于文档的**工具箱**更新以反映活动文档。  
  
- **编辑器**工具栏和**表**显示菜单和标题栏将更新以反映 Web 窗体的窗口。  
  
- 活动的层次结构窗口中，这通常是**解决方案资源管理器**，和标题栏更新以反映当前的上下文和上下文相关**项目**菜单命令现在将应用于活动站点应用程序项目。  
  
## <a name="see-also"></a>请参阅  
 [所选内容和 IDE 中的货币](../../extensibility/internals/selection-and-currency-in-the-ide.md)   
 [选择上下文对象](../../extensibility/internals/selection-context-objects.md)   
 [层次结构和选择](../../extensibility/internals/hierarchies-and-selection.md)
