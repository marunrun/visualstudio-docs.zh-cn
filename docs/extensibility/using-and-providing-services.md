---
title: 使用并提供服务 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- examples [Visual Studio SDK], services
- Visual Studio, services
- services
ms.assetid: c0b415ba-b825-4da0-9faf-8a60a663e302
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1c9b0dbf2122b5a76d557cdd70da27660b886041
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66337044"
---
# <a name="using-and-providing-services"></a>使用并提供服务
服务是两个 Vspackage 之间的协定。 一个 VSPackage 提供了一组特定的另一个 VSPackage 来使用的接口。 例如，[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]提供了<xref:Microsoft.VisualStudio.Shell.Interop.SVsActivityLog>服务到任何 VSPackage 它加载。 此服务提供<xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog>接口，可用于写入活动日志。 有关详细信息，请参阅[如何：使用活动日志](../extensibility/how-to-use-the-activity-log.md)。

 Vspackage 可以提供其自己的使用的服务<xref:Microsoft.VisualStudio.Shell.Interop.IProfferService>接口...

 Visual Studio 提供了重要的服务，如下所示：

|IDE 服务|描述|
|-----------------|-----------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>|提供了访问 IDE 的基本功能、 Vspackage、 与注册表服务处理。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>|提供了基本窗口化和在 IDE 中，如创建工具和文档窗口的功能与 UI 相关的功能。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>|提供了基本解决方案相关的功能，例如用于枚举项目、 创建新项目，以及监视项目的更改的功能。|

## <a name="in-this-section"></a>本节内容
- [服务基础知识](../extensibility/internals/service-essentials.md)显示 Visual Studio 服务的重要元素。

- [如何：获取服务](../extensibility/how-to-get-a-service.md)讨论了如何请求 （使用） 服务。

- [如何：提供的服务](../extensibility/how-to-provide-a-service.md)讨论如何提供服务。

- [如何：提供异步 Visual Studio 服务](../extensibility/how-to-provide-an-asynchronous-visual-studio-service.md)讨论如何提供异步服务。

- [如何：排查服务问题](../extensibility/how-to-troubleshoot-services.md)讨论常见的问题并提供了这些解决方案。

## <a name="related-sections"></a>相关章节
- [Visual Studio SDK](../extensibility/visual-studio-sdk.md)