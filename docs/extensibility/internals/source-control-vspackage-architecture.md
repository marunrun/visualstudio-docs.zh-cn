---
title: 源代码管理 VSPackage 体系结构 |Microsoft Docs
description: 了解源代码管理包的体系结构，它是一个 VSPackage，它提供 Visual Studio 的功能作为源代码管理服务。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control packages, architecture
ms.assetid: 453125fc-23dc-49b1-8476-94581f05e6c7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c03482ff489c356ddcbe28ccc26c69c5936be6c5
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2021
ms.locfileid: "97877671"
---
# <a name="source-control-vspackage-architecture"></a>源代码管理 VSPackage 体系结构
源代码管理包是使用 IDE 提供的服务的 VSPackage [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 在返回时，源代码管理包将其功能作为源代码管理服务提供。 此外，源代码管理包的替代方法比用于将源代码管理集成到的源代码管理插件更通用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

 实现源代码管理插件 API 的源代码管理插件 API 由严格协定遵守美国。 例如，插件不能 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] (UI) 替换默认用户界面。 此外，源代码管理插件 API 不会启用插件来实现其自己的源代码管理模型。 但源代码管理包克服了这两个限制。 源代码管理包完全控制用户的源代码管理体验 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 此外，源代码管理包可以使用其自己的源代码管理模型和逻辑，并可以定义所有与源代码管理相关的用户界面。

## <a name="source-control-package-components"></a>Source-Control 包组件
 如体系结构关系图中所示， [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 名为源代码管理存根的组件是一种集成了源代码管理包的 VSPackage [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

 源代码管理存根处理以下任务。

- 提供源控制包注册所需的公共 UI。

- 加载源代码管理包。

- 将源代码管理包设置为活动/非活动。

  源代码管理存根查找源控制包的活动服务，并将 IDE 中的所有传入服务调用路由到该程序包。

  源代码管理适配器包是提供的特殊源代码管理包 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 此包是支持基于源代码管理插件 API 的源代码管理插件的中心组件。 当源代码管理插件为活动插件时，源代码管理存根会将其事件发送到源代码管理适配器包。 接下来，源代码管理适配器包通过使用源代码管理插件 API 与源代码管理插件通信，还提供了一个适用于所有源代码管理插件的默认 UI。

  另一方面，如果源代码管理包是活动包，则源代码管理存根会使用 Source-Control 包接口直接与包通信 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 。 源代码管理包负责承载其自己的源代码管理 UI。

  ![源代码管理体系结构图](../../extensibility/internals/media/vsipsccarch.gif "VSIPSCCArch")

  对于源代码管理包，不 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 提供源代码管理代码或用于集成的 API。 与 [创建源代码](../../extensibility/internals/creating-a-source-control-plug-in.md) 管理插件（源代码管理插件必须实现一组严格的函数和回调）中所述的方法相比，这一点比较。

  与任何 VSPackage 一样，源代码管理包也是可以使用创建的 COM 对象 `CoCreateInstance` 。 VSPackage 通过实现来使自身可用于 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage> 。 创建实例后，VSPackage 将收到一个站点指针和一个 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> 接口，该接口提供对 IDE 中可用服务和接口的 VSPackage 访问。

  与编写源代码管理插件基于 API 的插件相比，编写基于 VSPackage 的源代码管理包需要更高级的编程专业技能。

## <a name="see-also"></a>另请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>
- [入门](../../extensibility/internals/getting-started-with-source-control-vspackages.md)
