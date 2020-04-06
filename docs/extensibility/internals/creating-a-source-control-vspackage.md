---
title: 创建源代码管理 VS 包 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], creating source control packages
- source control packages
ms.assetid: cca0a9ed-48ff-409f-8036-ed8db0f7533e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8608aae718ff9f8bdf2e40c0ab648c1d22c38257
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709195"
---
# <a name="create-a-source-control-vspackage"></a>创建源代码管理 VS 包
本文档包括指向与[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]集成的源代码管理包的体系结构概述的链接、由要实现的接口定义的 API 和要使用的服务，以及说明简单源代码管理包实现的示例。

 使用源代码管理 VSPackage，您可以创建深度集成路径，以便源代码管理与[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]集成。 它使包能够绕过由 承载的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]默认源代码管理 UI，响应来自项目系统的源代码管理请求，并与[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]**解决方案资源管理器**等组件进行交互。 授权[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)][!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]合作伙伴创建 VSPackage 的机制，该功能可与[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]使用服务模型集成。

## <a name="in-this-section"></a>在本节中
- [入门](../../extensibility/internals/getting-started-with-source-control-vspackages.md)

 讨论源代码管理包，它是源代码管理插件的更高级替代方法，用于在 中[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]实现源代码管理功能。

- [体系结构](../../extensibility/internals/source-control-vspackage-architecture.md)

 提供关系图并解释源代码管理包的组件。

- [功能](../../extensibility/internals/source-control-vspackage-features.md)

 描述源代码管理包的各种功能。

- [设计元素](../../extensibility/internals/source-control-vspackage-design-elements.md)

 描述源代码管理包必须实现的 VS 包的结构，以便进行深度集成。

## <a name="related-sections"></a>相关章节
- [创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)

 讨论如何创建源代码管理插件，在[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]源代码管理用户界面 （UI） 中提供源代码管理功能。

- [源代码管理](../../extensibility/internals/source-control.md)

 讨论了实现源代码管理作为 的集成功能的选项[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。
