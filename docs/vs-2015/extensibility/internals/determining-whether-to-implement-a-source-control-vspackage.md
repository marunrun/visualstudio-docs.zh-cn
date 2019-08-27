---
title: 确定是否实现源代码管理 VSPackage |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control packages, about source control packages
ms.assetid: 60b3326e-e7e2-4729-95fc-b682e7ad5c99
caps.latest.revision: 25
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: cff53700dcd6a80f841108d5a2b486dcb0ba7a11
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68196802"
---
# <a name="determining-whether-to-implement-a-source-control-vspackage"></a>确定是否实现源代码管理 VSPackage
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

本部分将详细介绍所选的源控制插件和源代码管理 Vspackage 扩展源代码管理解决方案，并提供全面的指南有关选择合适的集成路径。  
  
## <a name="small-source-control-solution-with-limited-resources"></a>资源有限的小型源控制解决方案  
 如果有限资源，并且不能承受编写源代码管理包的开销，你可以创建基于源控制插件 API 的插件。这使您可以与源代码管理包并行工作，可以切换源代码管理插件和按需包。 有关详细信息，请参阅[注册和选择](../../extensibility/internals/registration-and-selection-source-control-vspackage.md)。  
  
## <a name="large-source-control-solution-with-a-rich-feature-set"></a>具有丰富功能集的大的源代码控制解决方案  
 如果你想要实现提供了丰富的源控件模型，不使用源控制插件 API 充分捕获的源控制解决方案，则可以作为集成路径考虑源代码管理包。 这适用于尤其是，而是将替换源控件适配器包 （这与源代码管理插件进行通信并提供了一个基本的源控件 UI） 用您自己，这样可以自定义的方式处理源控件事件。 如果已有令人满意的源控件用户界面，并且想要保留这种体验[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]，源代码管理包选项可让你做到这一点。 源代码管理包不是泛型方法，并仅用于与一起使用[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]IDE。  
  
 如果你想要实现源控件解决方案，以提供灵活性和更丰富控制的源控制逻辑和 UI，您可能更倾向于源代码控制包集成路由。 你可以：  
  
1. 注册您自己的源代码管理 VSPackage (请参阅[注册和选择](../../extensibility/internals/registration-and-selection-source-control-vspackage.md))。  
  
2. 默认的源代码管理 UI 替换为你的自定义 UI (请参阅[自定义用户界面](../../extensibility/internals/custom-user-interface-source-control-vspackage.md))。  
  
3. 指定字形来使用和处理解决方案资源管理器标志符号事件 (请参阅[字形控件](../../extensibility/internals/glyph-control-source-control-vspackage.md))。  
  
4. 处理查询编辑和保存查询的事件 (请参阅[查询编辑查询保存](../../extensibility/internals/query-edit-query-save-source-control-vspackage.md))。  
  
## <a name="see-also"></a>请参阅  
 [创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)
