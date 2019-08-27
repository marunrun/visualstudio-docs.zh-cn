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
ms.openlocfilehash: 6f853f71428086f6c144c352e18e51f3f55c4d00
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66322533"
---
# <a name="source-control-integration-essentials"></a>源代码管理集成基础知识
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 支持两种类型的源代码管理集成： 提供基本功能，并且使用源控制插件 API （前称 MSSCCI API） 和基于 VSPackage 的源代码控制集成解决方案生成了源代码管理插件的提供了更强大的功能。

## <a name="source-control-plug-in"></a>源代码管理插件
 源代码管理插件编写为 DLL 实现源控件插件 API。 通过 API 提供注册和源代码控制集成功能。 这种方法是更轻松地实现比源代码管理 VSPackage，并且它使用[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]大多数源代码管理操作的用户界面 (UI)。

 若要实现源代码管理插件使用源控制插件 API，请执行以下步骤：

1. 创建实现中所指定的函数的 DLL[源代码管理插件](../../extensibility/source-control-plug-ins.md)。

2. 相应的注册表项，从而注册该 DLL，如中所述[如何：安装源代码管理插件](../../extensibility/internals/how-to-install-a-source-control-plug-in.md)。

3. 创建帮助器 UI 并将其通过源控件适配器包出现提示时显示 ([!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]处理通过源代码管理插件的源代码管理功能的组件)。

   有关详细信息，请参阅[创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)。

## <a name="source-control-vspackage"></a>源代码管理 VSPackage
 源代码管理 VSPackage 实现可用于开发的自定义的替换[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]源代码管理 UI。 此方法提供了完全控制源代码管理集成，但它要求您提供了 UI 元素，否则将下都能提供的插件方法的源代码控制接口实现。

 若要实现源代码管理 VSPackage，你必须：

1. 创建并注册您自己的源代码管理 VSPackage，如中所述[注册和选择](../../extensibility/internals/registration-and-selection-source-control-vspackage.md)。

2. 使用自定义 UI 替换默认的源代码管理 UI。 请参阅[自定义用户界面](../../extensibility/internals/custom-user-interface-source-control-vspackage.md)。

3. 指定字形来使用，并处理**解决方案资源管理器**标志符号的事件。 请参阅[字形控件](../../extensibility/internals/glyph-control-source-control-vspackage.md)。

4. 处理查询编辑和保存查询的事件，如中所示[查询编辑查询保存](../../extensibility/internals/query-edit-query-save-source-control-vspackage.md)。

   有关详细信息，请参阅[创建源代码管理 VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md)。

## <a name="see-also"></a>请参阅
- [概述](../../extensibility/internals/source-control-integration-overview.md)
- [创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)
- [创建源代码管理 VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md)