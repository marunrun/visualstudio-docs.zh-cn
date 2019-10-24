---
title: 源代码管理集成基础知识 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Source Control Integration, essentials
- Source Control Integration,overview
- essentials, Source Control Integration
ms.assetid: 442057cb-fd54-4283-96f8-2f6dc8bf2de7
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fcce3d8fdcc1c99c9b91bfebec572033ff3beb1a
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72723464"
---
# <a name="source-control-integration-essentials"></a>源代码管理集成基础知识
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 支持两种类型的源代码管理集成：源代码管理插件，提供基本功能，并使用源代码管理插件 API （以前称为 MSSCCI API）和基于 VSPackage 的源代码管理集成解决方案生成。这提供了更强大的功能。

## <a name="source-control-plug-in"></a>源代码管理插件
 源代码管理插件作为实现源代码管理插件 API 的 DLL 编写。 注册和源代码管理集成功能是通过 API 提供的。 与源代码管理 VSPackage 相比，此方法更容易实现，并且它使用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 用户界面（UI）来执行大多数源代码管理操作。

 若要使用源代码管理插件 API 实现源代码管理插件，请执行以下步骤：

1. 创建一个 DLL，该 DLL 实现[源代码管理插件](../../extensibility/source-control-plug-ins.md)中指定的函数。

2. 按照[如何：安装源代码管理插件](../../extensibility/internals/how-to-install-a-source-control-plug-in.md)中所述，通过创建适当的注册表项来注册 DLL。

3. 创建帮助器 UI，并在源代码管理适配器包（通过源代码管理插件处理源代码管理功能的 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 组件）提示时显示该 UI。

   有关详细信息，请参阅[创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)。

## <a name="source-control-vspackage"></a>源代码管理 VSPackage
 源代码管理 VSPackage 实现允许您为 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 源代码管理 UI 开发自定义的替换。 此方法提供对源代码管理集成的完全控制，但它要求您提供 UI 元素并实现源代码管理接口，否则将在插件方法下提供此方法。

 若要实现源代码管理 VSPackage，必须执行以下操作：

1. 按照[注册和选择](../../extensibility/internals/registration-and-selection-source-control-vspackage.md)中所述，创建并注册自己的源代码管理 VSPackage。

2. 将默认源代码管理 UI 替换为自定义 UI。 请参阅[自定义用户界面](../../extensibility/internals/custom-user-interface-source-control-vspackage.md)。

3. 指定要使用的标志符号，并处理**解决方案资源管理器**标志符号事件。 请参阅[标志符号控件](../../extensibility/internals/glyph-control-source-control-vspackage.md)。

4. 处理查询编辑和查询保存事件，如[查询编辑查询保存](../../extensibility/internals/query-edit-query-save-source-control-vspackage.md)中所示。

   有关详细信息，请参阅[创建源代码管理 VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md)。

## <a name="see-also"></a>请参阅
- [概述](../../extensibility/internals/source-control-integration-overview.md)
- [创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)
- [创建源代码管理 VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md)