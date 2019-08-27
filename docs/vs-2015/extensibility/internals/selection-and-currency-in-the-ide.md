---
title: 所选内容和 IDE 中的货币 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- currency, Visual Studio IDE
- IDE, selection
- selection, Visual Studio IDE
- IDE, currency
ms.assetid: 2f6f18d1-acd8-454d-a856-9a4d81155052
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d0a0b999a1a6e6ed2364060031f68378e7222ec0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68155820"
---
# <a name="selection-and-currency-in-the-ide"></a>IDE 中的选择和货币
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]集成的开发环境 (IDE) 维护有关用户的信息当前所选对象，通过使用所选内容*上下文*。 使用选定内容上下文的 Vspackage 可以参与货币跟踪两种方式：  
  
- 通过将传播到 IDE Vspackage 的货币信息。  
  
- 通过监视用户的当前处于活动状态的选择在 IDE 中。  
  
## <a name="selection-context"></a>选定内容上下文  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] IDE 全局跟踪的 IDE 在其自己的全局选择上下文对象中的货币。 下表显示了选定内容上下文构成元素。  
  
|元素|描述|  
|-------------|-----------------|  
|当前层次结构|通常在当前项目;NULL 当前层次结构指示作为一个整体解决方案是最新。|  
|当前 ItemID|当前层次结构; 内的选定的项如果有多个项目窗口中的选择，可以有多个当前项。|  
|当前 `SelectionContainer`|包含一个或多个对象为其属性窗口应显示属性。|  
  
 此外，环境负责维护两个全局列表：  
  
- Active UI 命令标识符的列表  
  
- 当前处于活动状态的元素类型的列表。  
  
### <a name="window-types-and-selection"></a>窗口类型和所选内容  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] IDE 将 windows 组织到两种常规类型：  
  
- 层次结构类型 windows  
  
- 框架窗口，如工具和文档窗口  
  
  IDE 以不同的方式跟踪的每个窗口类型的货币。  
  
  最常见的项目类型窗口是解决方案资源管理器，它控制 IDE。 项目类型窗口跟踪的全局层次结构和 ItemID 的全局选择上下文，并在窗口依赖于用户的选择来确定当前层次结构。 对于项目类型 windows 环境提供了全局服务<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>，通过的 Vspackage 可以监视打开的元素的当前值。 在环境中浏览的属性取决于此全局服务。  
  
  框架窗口，但是，使用该文档框架窗口内推送 SelectionContext 值 （层次结构/ItemID/SelectionContainer 三个）。 . 框架窗口使用服务<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>实现此目的。 该文档可以推送仅为所选内容容器的值保留本地值的层次结构和 ItemID 不变，因为是典型的 MDI 子文档。  
  
### <a name="events-and-currency"></a>事件和货币  
 两种类型的事件可能会发生，会影响环境的这一概念的货币：  
  
- 传播到全局级别和更改窗口框架选定内容上下文的事件。 此类事件的示例包括全局工具窗口处于打开或正在打开的项目类型工具窗口处于打开的 MDI 子窗口。  
  
- 更改跟踪的窗口框架选择上下文中的元素的事件。 示例包括更改所选内容内 DocObject 或更改项目类型窗口中的选择。  
  
## <a name="see-also"></a>请参阅  
 [选择上下文对象](../../extensibility/internals/selection-context-objects.md)   
 [为用户提供反馈](../../extensibility/internals/feedback-to-the-user.md)
