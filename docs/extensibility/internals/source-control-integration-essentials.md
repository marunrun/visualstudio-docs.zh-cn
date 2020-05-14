---
title: 源代码管理集成要点 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Source Control Integration, essentials
- Source Control Integration,overview
- essentials, Source Control Integration
ms.assetid: 442057cb-fd54-4283-96f8-2f6dc8bf2de7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e56658d644720f1563d71d3d08bf35268119112f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705235"
---
# <a name="source-control-integration-essentials"></a>源代码管理集成基础知识
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]支持两种类型的源代码管理集成：一种是源代码管理插件，提供基本功能，并使用源代码管理插件 API（以前称为 MSSCCI API）构建，另一种基于 VSPackage 的源代码管理集成解决方案提供更强大的功能。

## <a name="source-control-plug-in"></a>源代码管理插件
 源代码管理插件编写为 DLL，用于实现源代码管理插件 API。 注册和源代码管理集成功能通过 API 提供。 此方法比源代码管理 VSPackage 更容易实现，并且它使用[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]用户界面 （UI） 执行大多数源代码管理操作。

 要使用源代码管理插件 API 实现源代码管理插件，请按照以下步骤操作：

1. 创建实现[源代码管理插件](../../extensibility/source-control-plug-ins.md)中指定的函数的 DLL。

2. 通过创建适当的注册表项注册 DLL，如["如何：安装源代码管理插件](../../extensibility/internals/how-to-install-a-source-control-plug-in.md)"中所述。

3. 创建帮助程序 UI 并在源代码管理适配器包（通过源代码管理插件处理源代码[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]管理功能的组件）提示时显示它。

   有关详细信息，请参阅[创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)。

## <a name="source-control-vspackage"></a>源代码管理 VS 包
 源代码管理 VSPackage 实现允许您为[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]源代码管理 UI 开发自定义替换。 此方法提供对源代码管理集成的完全控制，但它要求您提供 UI 元素并实现在插件方法下提供的源代码管理接口。

 要实现源代码管理 VSPackage，您必须：

1. 创建并注册您自己的源代码管理 VSPackage，如[注册和选择](../../extensibility/internals/registration-and-selection-source-control-vspackage.md)中所述。

2. 将默认源代码管理 UI 替换为自定义 UI。 请参阅[自定义用户界面](../../extensibility/internals/custom-user-interface-source-control-vspackage.md)。

3. 指定要使用的字形，并处理**解决方案资源管理器**字形事件。 请参阅[字形控件](../../extensibility/internals/glyph-control-source-control-vspackage.md)。

4. 处理查询编辑和查询保存事件，如[查询编辑查询保存 中](../../extensibility/internals/query-edit-query-save-source-control-vspackage.md)所示。

   有关详细信息，请参阅[创建源代码管理 VS 包](../../extensibility/internals/creating-a-source-control-vspackage.md)。

## <a name="see-also"></a>请参阅
- [概述](../../extensibility/internals/source-control-integration-overview.md)
- [创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)
- [创建源代码管理 VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md)
