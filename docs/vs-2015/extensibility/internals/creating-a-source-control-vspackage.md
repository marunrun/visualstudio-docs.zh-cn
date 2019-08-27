---
title: 创建源代码管理 VSPackage |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], creating source control packages
- source control packages
ms.assetid: cca0a9ed-48ff-409f-8036-ed8db0f7533e
caps.latest.revision: 24
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2b1516cf358a4488ff02e650f6c703a1761a94a2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68196953"
---
# <a name="creating-a-source-control-vspackage"></a>创建源代码管理 VSPackage
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

本文档包括指向与集成的源代码管理包的体系结构概述[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]，定义要实现的接口和服务将使用的 API 和示例演示一个简单的源控制包实现。  
  
 可以使用源代码管理 VSPackage，创建源代码管理与集成的深度集成路径[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。 它使包能够绕过默认源控件 UI 由承载[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]、 响应的源控件请求的项目系统，并与交互[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]组件，例如**解决方案资源管理器**。 [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)]使[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]具有一种机制来创建的 VSPackage 可以与集成的合作伙伴[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]使用服务模型。  
  
## <a name="in-this-section"></a>本节内容  
 [入门](../../extensibility/internals/getting-started-with-source-control-vspackages.md)  
 讨论了源代码管理包，这是源代码管理插件实现中的源代码管理功能的更高级的替代[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。  
  
 [体系结构](../../extensibility/internals/source-control-vspackage-architecture.md)  
 显示关系图并解释了源代码管理包的组件。  
  
 [功能](../../extensibility/internals/source-control-vspackage-features.md)  
 介绍的各种功能的源代码管理包。  
  
 [设计元素](../../extensibility/internals/source-control-vspackage-design-elements.md)  
 介绍源代码管理包必须实现的深度集成的 VSPackage 的结构。  
  
## <a name="related-sections"></a>相关章节  
 [创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)  
 讨论如何创建一个源代码管理插件提供的源代码管理功能中[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]源代码管理用户界面 (UI)。  
  
 [源代码管理](../../extensibility/internals/source-control.md)  
 讨论用于实现源控件的集成功能作为选项[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。
