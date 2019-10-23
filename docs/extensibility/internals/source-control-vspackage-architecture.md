---
title: 源代码管理 VSPackage 体系结构 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control packages, architecture
ms.assetid: 453125fc-23dc-49b1-8476-94581f05e6c7
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9484aabd0080b0a44d75a8a5f6d90d9217d74b8e
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72723351"
---
# <a name="source-control-vspackage-architecture"></a>源代码管理 VSPackage 体系结构
源代码管理包是一个 VSPackage，它使用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE 提供的服务。 在返回时，源代码管理包将其功能作为源代码管理服务提供。 此外，源代码管理包是一个比源代码管理插件更通用的替代方法，用于将源代码管理集成到 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 中。

 实现源代码管理插件 API 的源代码管理插件 API 由严格协定遵守美国。 例如，插件不能替换默认 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 用户界面（UI）。 此外，源代码管理插件 API 不会启用插件来实现其自己的源代码管理模型。 但源代码管理包克服了这两个限制。 源代码管理包对 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 用户的源代码管理体验具有完全控制。 此外，源代码管理包可以使用其自己的源代码管理模型和逻辑，并可以定义所有与源代码管理相关的用户界面。

## <a name="source-control-package-components"></a>源代码管理包组件
 如体系结构关系图中所示，名为源代码管理存根的 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 组件是一个将源代码管理包与 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 集成的 VSPackage。

 源代码管理存根处理以下任务。

- 提供源控制包注册所需的公共 UI。

- 加载源代码管理包。

- 将源代码管理包设置为活动/非活动。

  源代码管理存根查找源控制包的活动服务，并将 IDE 中的所有传入服务调用路由到该程序包。

  源代码管理适配器包是 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 提供的特殊源代码管理包。 此包是支持基于源代码管理插件 API 的源代码管理插件的中心组件。 当源代码管理插件为活动插件时，源代码管理存根会将其事件发送到源代码管理适配器包。 接下来，源代码管理适配器包通过使用源代码管理插件 API 与源代码管理插件通信，还提供了一个适用于所有源代码管理插件的默认 UI。

  另一方面，如果源代码管理包是活动包，则源代码管理存根会使用 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 源代码管理包接口直接与包通信。 源代码管理包负责承载其自己的源代码管理 UI。

  ![源代码管理体系结构图形](../../extensibility/internals/media/vsipsccarch.gif "VSIPSCCArch")

  对于源代码管理包，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 不提供源代码管理代码或用于集成的 API。 与[创建源代码](../../extensibility/internals/creating-a-source-control-plug-in.md)管理插件（源代码管理插件必须实现一组严格的函数和回调）中所述的方法相比，这一点比较。

  与任何 VSPackage 一样，源代码管理包也是可使用 `CoCreateInstance` 创建的 COM 对象。 VSPackage 通过实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage> 使自身对 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE 可用。 创建实例后，VSPackage 将收到一个站点指针和一个 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> 接口，该接口提供对 IDE 中可用服务和接口的 VSPackage 访问。

  与编写源代码管理插件基于 API 的插件相比，编写基于 VSPackage 的源代码管理包需要更高级的编程专业技能。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>
- [入门](../../extensibility/internals/getting-started-with-source-control-vspackages.md)