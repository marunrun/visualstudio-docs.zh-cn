---
title: 确定是否实现源代码管理 VSPackage |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control packages, about source control packages
ms.assetid: 60b3326e-e7e2-4729-95fc-b682e7ad5c99
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ba0ac240c8b8a93b6afbf1ec7dd580090ee54fd9
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66351614"
---
# <a name="determine-whether-to-implement-a-source-control-vspackage"></a>确定是否实现源代码管理 VSPackage
本部分将详细介绍所选的源控制插件和源代码管理 Vspackage 扩展源代码管理解决方案，并提供全面的指南有关选择合适的集成路径。

## <a name="small-source-control-solution-with-limited-resources"></a>资源有限的小型源控制解决方案
 如果有限资源，并且不能承受编写源代码管理包的开销，你可以创建基于源控制插件 API 的插件。这样做使您能够与源代码管理包，并可以切换源代码管理插件和按需包。 有关详细信息，请参阅[注册和选择](../../extensibility/internals/registration-and-selection-source-control-vspackage.md)。

## <a name="large-source-control-solution-with-a-rich-feature-set"></a>使用丰富的功能集的大的源代码控制解决方案
 如果你想要实现提供了丰富的源控件模型，不使用源控制插件 API 充分捕获的源控制解决方案，则可以作为集成路径考虑源代码管理包。 这适用于尤其是，而是将替换源控件适配器包 （这与源代码管理插件进行通信并提供了一个基本的源控件 UI） 用您自己，这样可以自定义的方式处理源控件事件。 如果已有令人满意的源控件用户界面，并且想要保留这种体验[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]，源代码管理包选项可让你做到这一点。 源代码管理包不是泛型方法，并仅用于与一起使用[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]IDE。

 如果你想要实现源控件解决方案，以提供灵活性和更丰富控制的源控制逻辑和 UI，您可能更倾向于源代码控制包集成路由。 你可以：

1. 注册您自己的源代码管理 VSPackage (请参阅[注册和选择](../../extensibility/internals/registration-and-selection-source-control-vspackage.md))。

2. 默认的源代码管理 UI 替换为你的自定义 UI (请参阅[自定义用户界面](../../extensibility/internals/custom-user-interface-source-control-vspackage.md))。

3. 指定字形来使用和处理解决方案资源管理器标志符号事件 (请参阅[字形控件](../../extensibility/internals/glyph-control-source-control-vspackage.md))。

4. 处理查询编辑和保存查询的事件 (请参阅[查询编辑查询保存](../../extensibility/internals/query-edit-query-save-source-control-vspackage.md))。

## <a name="see-also"></a>请参阅
- [创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)