---
title: 使用和提供服务 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- examples [Visual Studio SDK], services
- Visual Studio, services
- services
ms.assetid: c0b415ba-b825-4da0-9faf-8a60a663e302
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8741d8d66af96ad4c6abea44b238393a34c5aa95
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80698737"
---
# <a name="using-and-providing-services"></a>使用并提供服务
服务是两个 VSPackages 之间的协定。 一个 VSPackage 提供了一组特定的接口，供另一个 VSPackage 使用。 例如，[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]向<xref:Microsoft.VisualStudio.Shell.Interop.SVsActivityLog>它加载的任何 VSPackage 提供服务。 此服务提供<xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog>接口，该接口可用于写入活动日志。 有关详细信息，请参阅[：使用活动日志](../extensibility/how-to-use-the-activity-log.md)。

 VSPackages 可以使用<xref:Microsoft.VisualStudio.Shell.Interop.IProfferService>接口提供自己的服务。

 Visual Studio 提供重要的服务，例如：

|IDE 服务|描述|
|-----------------|-----------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>|提供对处理基本功能、VS 包和注册表的 IDE 服务的访问。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>|在 IDE 中提供基本窗口和与 UI 相关的功能，例如创建工具和文档窗口的功能。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>|提供与解决方案相关的基本功能，例如枚举项目、创建新项目和监视项目更改的能力。|

## <a name="in-this-section"></a>本节内容
- [服务要点](../extensibility/internals/service-essentials.md)呈现视觉工作室服务的重要元素。

- [如何：获取服务](../extensibility/how-to-get-a-service.md)讨论如何请求（使用）服务。

- [如何：提供服务](../extensibility/how-to-provide-a-service.md)讨论如何提供服务。

- [如何：提供异步视觉工作室服务](../extensibility/how-to-provide-an-asynchronous-visual-studio-service.md)讨论如何提供异步服务。

- [如何：故障排除服务](../extensibility/how-to-troubleshoot-services.md)讨论常见问题并提出解决方案。

## <a name="related-sections"></a>相关章节
- [Visual Studio SDK](../extensibility/visual-studio-sdk.md)
