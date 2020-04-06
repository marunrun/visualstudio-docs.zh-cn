---
title: 源代码管理 VS 包架构 |微软文档
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
ms.openlocfilehash: d6e62aa9e2d725e982f0605e2721f0bfeb3cc5ee
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705082"
---
# <a name="source-control-vspackage-architecture"></a>源代码管理 VSPackage 体系结构
源代码管理包是使用 IDE 提供的服务的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]VS 包。 作为回报，源代码管理包提供其功能作为源代码管理服务。 此外，源代码管理包是一种比源代码管理插件更通用的替代方法，用于将源代码管理集成到 中[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。

 实现源代码管理插件 API 的源代码管理插件遵守严格的协定。 例如，插件不能替换默认[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]用户界面 （UI）。 此外，源代码管理插件 API 不能启用插件来实现其自己的源代码管理模型。 但是，源代码管理包克服了这两个限制。 源代码管理包可以完全控制[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]用户的源代码管理体验。 此外，源代码管理包可以使用自己的源代码管理模型和逻辑，并且它可以定义所有与源代码管理相关的用户界面。

## <a name="source-control-package-components"></a>源代码管理包组件
 如体系结构图所示，名为源代码管理[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]存根的组件是一个 VSPackage，它将源代码管理包与 集成[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]在一起。

 源代码管理存根处理以下任务。

- 提供源代码管理包注册所需的通用 UI。

- 加载源代码管理包。

- 将源代码管理包设为活动/非活动。

  源代码管理存根查找源代码管理包的活动服务，并将所有传入服务呼叫从 IDE 路由到该包。

  源代码管理适配器包是[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]提供的特殊源代码管理包。 此包是基于源代码管理插件 API 支持源代码管理插件的中心组件。 当源代码管理插件是活动插件时，源代码管理存根会将其事件发送到源代码管理适配器包。 反过来，源代码管理适配器包通过使用源代码管理插件 API 与源代码管理插件通信，并提供适用于所有源代码管理插件的默认 UI。

  另一方面，当源代码管理包是活动包时，源代码管理存根通过使用[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]源代码管理包接口直接与包通信。 源代码管理包负责托管自己的源代码管理 UI。

  ![源代码管理体系结构图](../../extensibility/internals/media/vsipsccarch.gif "VSIPSCCArch")

  对于源代码管理包，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]不提供源代码或 API 进行集成。 与[创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)中概述的方法形成对比，其中源代码管理插件必须实现一组严格的函数和回调。

  与任何 VSPackage 一样，源代码管理包是可以使用`CoCreateInstance`创建的 COM 对象。 VS包通过实现[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>来使自己对 IDE 可用。 创建实例后，VSPackage 将接收站点指针和接口<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>，该接口提供对 IDE 中可用服务和接口的 VSPackage 访问权限。

  编写基于 VSPackage 的源代码管理包需要比编写基于源代码管理插件 API 的插件更高级的编程专业知识。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>
- [入门](../../extensibility/internals/getting-started-with-source-control-vspackages.md)
