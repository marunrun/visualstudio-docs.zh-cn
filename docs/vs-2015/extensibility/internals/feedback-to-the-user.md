---
title: 向用户提供反馈 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62537675"
---
# <a name="feedback-to-the-user"></a>为用户提供反馈
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

在 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 集成开发环境 (IDE) 上，有关可用功能的视觉反馈基于用户的当前选择和全局选择上下文。 下表列出了在不同选择上下文中可用的功能。  
  
|选择上下文|可用功能|  
|-----------------------|-----------------------------|  
|IDE|全球|  
|当前产品集|特定于产品|  
|活动层次结构|层次结构类型特定|  
|活动层次结构项|层次结构项类型特定|  
|活动文档|特定于文档类型|  
| (MDI) 窗口的最顶层多文档界面|特定于窗口类型|  
|当前选择上下文|特定于选择上下文|  
  
 如果只介绍用户需要的功能并持续提供一致的选择和环境上下文反馈，则可以降低 IDE 的复杂性。 在 IDE 中打开窗口时，下列规则适用：  
  
- 如果该窗口更改了其选择上下文，则在该窗口中清楚地指示了选择反馈，并且动态帮助窗口（如果已显示）将更新以反映当前的上下文。  
  
- 如果窗口更改全局选择上下文，则所有上下文特定的菜单、活动的层次结构窗口和应用程序标题栏都将更新，以反映当前的上下文。  
  
- 窗口应显示 " **属性** " 窗口中当前选定内容的表面属性，如果显示，还应显示 " **属性页** " 对话框。  
  
- 如果该窗口不是表面属性或更改全局选择上下文，则当它不再是 IDE 中的活动窗口时，选择反馈不会保留在窗口中。  
  
- 所有特定于文档的工具窗口应持续反映活动文档。  
  
- 菜单、工具栏和应用程序标题栏应反映 (MDI) 客户端窗口的最顶层多文档界面。  
  
  例如，当打开 Visual Basic Web 应用程序项目中的 Web 窗体的 HTML 视图，并且用户选择了一个标记时，将通过 `<td>` 以下方式提供反馈：  
  
- 在活动窗口中指定了选择，并反映在 " **属性** " 窗口中。  
  
- 文档特定的 **工具箱** 将更新以反映活动文档。  
  
- 将显示 **编辑器** 工具栏和 **表** 菜单，并且标题栏将更新以反映 Web 窗体窗口。  
  
- 活动层次结构窗口通常是 **解决方案资源管理器**的，其标题栏更新将反映当前上下文，并且上下文相关 **项目** 菜单命令现在适用于活动 Web 应用程序项目。  
  
## <a name="see-also"></a>另请参阅  
 [IDE 中的选择和货币](../../extensibility/internals/selection-and-currency-in-the-ide.md)   
 [选择上下文对象](../../extensibility/internals/selection-context-objects.md)   
 [层次结构和选择](../../extensibility/internals/hierarchies-and-selection.md)
