---
title: IDE 中的选择和货币 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- currency, Visual Studio IDE
- IDE, selection
- selection, Visual Studio IDE
- IDE, currency
ms.assetid: 2f6f18d1-acd8-454d-a856-9a4d81155052
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f580b7c8e1651dcbcd053476ae756399a0ac3482
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80705573"
---
# <a name="selection-and-currency-in-the-ide"></a>IDE 中的选择和货币
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]集成开发环境 (IDE) 使用选择*上下文*维护用户当前选择的对象的相关信息。 使用选择上下文，Vspackage 可以通过两种方式参与货币跟踪：

- 将有关 Vspackage 的货币信息传播到 IDE。

- 监视用户当前在 IDE 内处于活动状态的选定内容。

## <a name="selection-context"></a>选择上下文
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]Ide 全局地在其自己的全局选择上下文对象中跟踪 IDE 货币。 下表显示组成选择上下文的元素。

|元素|说明|
|-------------|-----------------|
|当前层次结构|通常为当前项目;空的当前层次结构表示整个解决方案是最新的。|
|当前 ItemID|当前层次结构中的选定项;如果项目窗口中有多个选择，则可以有多个当前项。|
|当前 `SelectionContainer`|保存一个或多个属性窗口应显示其属性的对象。|

 此外，环境维护两个全局列表：

- 活动 UI 命令标识符的列表

- 当前处于活动状态的元素类型的列表。

### <a name="window-types-and-selection"></a>窗口类型和选定内容
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]IDE 将窗口分为两种类型：

- 层次结构-类型窗口

- 框架窗口，如工具窗口和文档窗口

  IDE 会以不同的方式跟踪每个窗口类型的货币。

  最常见的项目类型窗口是 IDE 控制的解决方案资源管理器。 项目类型窗口跟踪全局选择上下文的全局层次结构和 ItemID，窗口依赖于用户的选择来确定当前层次结构。 对于项目类型窗口，环境提供了全局服务 <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> ，通过该服务，vspackage 可以监视开放式元素的当前值。 环境中的属性浏览由这一全局服务驱动。

  另一方面，框架窗口使用框架窗口中的 DocObject 将 SelectionContext 值推送 (层次结构/ItemID/SelectionContainer 三个) 。 . 框架 windows 使用该服务 <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> 实现此目的。 DocObject 可以仅推送选择容器的值，而将层次结构和 ItemID 的本地值保持不变，这对于 MDI 子文档而言是典型值。

### <a name="events-and-currency"></a>事件和货币
 可能会发生两种类型的事件，这些事件会影响环境的货币概念：

- 传播到全局级别并更改窗口框架选择上下文的事件。 此类事件的示例包括正在打开的 MDI 子窗口、打开的全局工具窗口或正在打开的项目类型工具窗口。

- 更改窗口框架选择上下文中所跟踪元素的事件。 示例包括更改 DocObject 中的选定内容或更改项目类型窗口中的选定内容。

## <a name="see-also"></a>另请参阅
- [选择上下文对象](../../extensibility/internals/selection-context-objects.md)
- [为用户提供反馈](../../extensibility/internals/feedback-to-the-user.md)
