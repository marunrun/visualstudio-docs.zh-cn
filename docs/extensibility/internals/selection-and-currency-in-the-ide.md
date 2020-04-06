---
title: IDE 中的选择和货币 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705573"
---
# <a name="selection-and-currency-in-the-ide"></a>IDE 中的选择和货币
集成[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]开发环境 （IDE） 使用选择*上下文*维护用户当前选择的对象的信息。 使用选择上下文，VSPackages 可通过两种方式参与货币跟踪：

- 通过将有关 VSPackages 的货币信息传播到 IDE。

- 通过监视用户当前在 IDE 中的活动选择。

## <a name="selection-context"></a>选择上下文
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE 全局跟踪其自己的全局选择上下文对象中的 IDE 货币。 下表显示了构成选择上下文的元素。

|元素|描述|
|-------------|-----------------|
|当前层次结构|通常是当前项目;NULL 电流层次结构表示整个解决方案是最新的。|
|当前项目 ID|当前层次结构中的选定项;当项目窗口中有多个选择时，可以有多个当前项。|
|当前`SelectionContainer`|保存属性窗口应为其显示属性的一个或多个对象。|

 此外，环境维护两个全局列表：

- 活动 UI 命令标识符的列表

- 当前活动元素类型的列表。

### <a name="window-types-and-selection"></a>窗口类型和选择
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE 将窗口组织成两种常规类型：

- 层次结构类型窗口

- 框架窗口，如工具和文档窗口

  IDE 对这些窗口类型的不同跟踪货币。

  最常见的项目类型窗口是 IDE 控制的解决方案资源管理器。 项目类型窗口跟踪全局选择上下文的全局层次结构和 ItemID，该窗口依赖于用户的选择来确定当前层次结构。 对于项目类型窗口，环境提供全局服务<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>，VS包可以通过该服务监视打开元素的当前值。 环境中的属性浏览由此全局服务驱动。

  另一方面，框架窗口使用框架窗口中的 DocObject 推送选择上下文值（层次结构/ItemID/选择容器三重奏）。 . 框架窗口为此使用服务<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>。 DocObject 只能推送选择容器的值，从而使层次结构和 ItemID 的本地值保持不变，这是 MDI 子文档的典型值。

### <a name="events-and-currency"></a>事件和货币
 可能发生两种类型的事件，这些事件会影响环境的货币概念：

- 传播到全局级别并更改窗口框架选择上下文的事件。 此类事件的示例包括正在打开的 MDI 子窗口、正在打开的全局工具窗口或正在打开的项目类型工具窗口。

- 更改窗口框架选择上下文中跟踪的元素的事件。 示例包括在 DocObject 中更改选择或在项目类型窗口中更改选择。

## <a name="see-also"></a>请参阅
- [选择上下文对象](../../extensibility/internals/selection-context-objects.md)
- [为用户提供反馈](../../extensibility/internals/feedback-to-the-user.md)
