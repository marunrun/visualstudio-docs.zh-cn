---
title: 创建源代码管理 VSPackage |Microsoft Docs
description: 了解如何创建一个源代码管理 VSPackage，用于创建要与 Visual Studio 集成的源代码管理的深度集成路径。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 69e526cea292544c725abc7ffb54d0b29ad88403
ms.sourcegitcommit: 2244665d5a0e22d12dd976417f2a782e68684705
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2020
ms.locfileid: "96305579"
---
# <a name="create-a-source-control-vspackage"></a>创建源代码管理 VSPackage
此文档包括以下内容的链接：与集成的源代码管理包的结构概述 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 、要实现的接口定义的 API 以及要使用的服务，以及阐释简单源代码管理包实现的示例。

 使用源代码管理 VSPackage，可以为源代码管理创建与集成的深度集成路径 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 它使包能够绕过承载的默认源代码管理 UI [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ，响应来自项目系统的源代码管理请求，并与 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] **解决方案资源管理器** 等组件进行交互。 为 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 合作伙伴提供一种机制，用于创建可 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 使用服务模型集成的 VSPackage。

## <a name="in-this-section"></a>在本节中
- [入门](../../extensibility/internals/getting-started-with-source-control-vspackages.md)

 讨论源代码管理包，它是源代码管理插件的一种更高级的替代项，用于实现中的源代码管理功能 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

- [体系结构](../../extensibility/internals/source-control-vspackage-architecture.md)

 显示一个关系图，并说明源代码管理包的组件。

- [功能](../../extensibility/internals/source-control-vspackage-features.md)

 描述源代码管理包的各种功能。

- [设计元素](../../extensibility/internals/source-control-vspackage-design-elements.md)

 描述源代码管理包为深度集成而必须实现的 VSPackage 的结构。

## <a name="related-sections"></a>相关章节
- [创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)

 讨论如何创建源代码管理插件，该插件在源代码管理用户界面中提供源代码管理功能， [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] (UI) 。

- [源代码管理](../../extensibility/internals/source-control.md)

 讨论用于实现作为的集成功能的源代码管理的选项 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。
