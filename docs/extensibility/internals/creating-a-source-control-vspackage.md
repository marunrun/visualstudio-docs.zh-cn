---
title: 创建源代码管理 VSPackage |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], creating source control packages
- source control packages
ms.assetid: cca0a9ed-48ff-409f-8036-ed8db0f7533e
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 259273eee51c74eb7cb5ca4534db9bc575fd1758
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66345489"
---
# <a name="create-a-source-control-vspackage"></a>创建源代码管理 VSPackage
本文档包括指向与集成的源代码管理包的体系结构概述[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]，定义要实现的接口和服务将使用的 API 和示例演示一个简单的源控制包实现。

 可以使用源代码管理 VSPackage，创建源代码管理与集成的深度集成路径[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。 它使包能够绕过默认源控件 UI 由承载[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]、 响应的源控件请求的项目系统，并与交互[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]组件，例如**解决方案资源管理器**。 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]使[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]具有一种机制来创建的 VSPackage 可以与集成的合作伙伴[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]使用服务模型。

## <a name="in-this-section"></a>本节内容
- [入门](../../extensibility/internals/getting-started-with-source-control-vspackages.md)

 讨论了源代码管理包，这是源代码管理插件实现中的源代码管理功能的更高级的替代[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。

- [体系结构](../../extensibility/internals/source-control-vspackage-architecture.md)

 显示关系图并解释了源代码管理包的组件。

- [功能](../../extensibility/internals/source-control-vspackage-features.md)

 介绍的各种功能的源代码管理包。

- [设计元素](../../extensibility/internals/source-control-vspackage-design-elements.md)

 介绍源代码管理包必须实现的深度集成的 VSPackage 的结构。

## <a name="related-sections"></a>相关章节
- [创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)

 讨论如何创建一个源代码管理插件提供的源代码管理功能中[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]源代码管理用户界面 (UI)。

- [源代码管理](../../extensibility/internals/source-control.md)

 讨论用于实现源控件的集成功能作为选项[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。
