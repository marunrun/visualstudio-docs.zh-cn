---
title: 确定是否实现源代码管理 VS 包 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control packages, about source control packages
ms.assetid: 60b3326e-e7e2-4729-95fc-b682e7ad5c99
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8707f3c1ced1cc2df9d3ae77280fc8779874a837
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708720"
---
# <a name="determine-whether-to-implement-a-source-control-vspackage"></a>确定是否实现源代码管理 VSPackage
本节详细介绍了源代码管理插件和源代码管理 VSPackages 用于扩展源代码管理解决方案的选择，并给出了有关选择适当集成路径的广泛指南。

## <a name="small-source-control-solution-with-limited-resources"></a>资源有限的小型源代码管理解决方案
 如果资源有限，并且无法承担编写源代码管理包的开销，则可以创建基于源代码管理插件的插件。这样做允许您与源代码管理包并行工作，并且可以按需在源代码管理插件和包之间切换。 有关详细信息，请参阅[注册和选择](../../extensibility/internals/registration-and-selection-source-control-vspackage.md)。

## <a name="large-source-control-solution-with-a-rich-feature-set"></a>具有丰富功能集的大型源代码管理解决方案
 如果要实现源控件解决方案，该解决方案提供丰富的源代码管理模型，但使用源代码管理插件 API 未充分捕获，则可以将源代码管理包视为集成路径。 这尤其适用于您希望将源代码管理适配器包（与源代码管理插件通信并提供基本源代码管理 UI）替换为您自己的，以便以自定义方式处理源代码管理事件。 如果您已经有一个令人满意的源代码管理 UI，并希望在 中[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]保留该体验，源代码管理包选项允许您做到这一点。 源代码管理包不是通用的，仅用于 IDE。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]

 如果要实现对源代码管理逻辑和 UI 提供灵活性和更丰富的控制的源代码管理解决方案，您可能更喜欢源代码管理包集成路由。 可以：

1. 注册您自己的源代码管理 VSPackage（请参阅[注册和选择](../../extensibility/internals/registration-and-selection-source-control-vspackage.md)）。

2. 将默认源代码管理 UI 替换为自定义 UI（请参阅[自定义用户界面](../../extensibility/internals/custom-user-interface-source-control-vspackage.md)）。

3. 指定要使用的字形并处理解决方案资源管理器字形事件（请参阅[字形控件](../../extensibility/internals/glyph-control-source-control-vspackage.md)）。

4. 处理查询编辑和查询保存事件（请参阅[查询编辑查询保存](../../extensibility/internals/query-edit-query-save-source-control-vspackage.md)）。

## <a name="see-also"></a>请参阅
- [创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)
