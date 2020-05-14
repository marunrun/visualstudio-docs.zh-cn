---
title: 源代码管理插件架构 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, architecture
ms.assetid: 35351d4c-9414-409b-98fc-f2023e2426b7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f549ad2c4ee456860a08fbf20ccda813934a8582
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705113"
---
# <a name="source-control-plug-in-architecture"></a>源代码管理插件体系结构
您可以通过实现和附加源代码管理插件，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]向集成开发环境 （IDE） 添加源代码管理支持。 IDE 通过定义良好的源代码管理插件 API 连接到源代码管理插件。 IDE 通过提供由工具栏和菜单命令组成的用户界面 （UI） 来公开源代码管理系统的版本控制功能。 源代码管理插件实现源代码管理功能。

## <a name="source-control-plug-in-resources"></a>源代码管理插件资源
 源代码管理插件提供资源来帮助创建版本控制应用程序并将其连接到[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]IDE。 源代码管理插件包含必须由源代码管理插件实现的 API 规范，以便它可以集成到 IDE 中[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。 它还包含一个代码示例（用 C++编写），该示例实现了骨架源代码管理插件，演示了符合源代码管理插件 API 的基本功能的实现。

 源代码管理插件 API 规范允许您利用您选择的任何源代码管理系统，如果您创建源代码管理 DLL 与根据源代码管理插件 API 实现所需的函数集。

## <a name="components"></a>组件
 关系图中的源代码管理适配器包是 IDE 的组件，该组件将用户对源代码管理操作的请求转换为源代码管理插件支持的函数调用。 要做到这一点，IDE 和源代码管理插件必须有一个有效的对话框，在 IDE 和插件之间来回传递信息。 要进行此对话框，它们都必须讲同一种语言。 本文档中概述的源代码管理插件 API 是此交换的常见词汇表。

 ![源代码控制体系结构图](../../extensibility/internals/media/vs_sccsdk_plug_in_arch.gif "vs_sccsdk_plug_in_arch")显示 VS 和源代码管理插件之间交互的体系结构图

 如体系结构图所示，在关系图[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]中标记为 VS shell 的 shell 承载用户的工作项目和相关组件（如编辑器和解决方案资源管理器）。 源代码管理适配器包处理 IDE 和源代码管理插件之间的交互。 源代码管理适配器包提供其自己的源代码管理 UI。 它是用户交互以启动和定义源代码管理操作范围的顶级 UI。

 源代码管理插件可以有自己的 UI，该 UI 可能由图中的两个部分组成。 标记为"供应商 UI"的框表示您作为源代码管理插件创建者提供的自定义用户界面元素。 当用户调用高级源代码管理操作时，源代码管理插件会直接显示这些操作。 标记为"帮助者 UI"的框是一组通过 IDE 间接调用的源代码管理插件 UI 功能。 源代码管理插件通过 IDE 提供的特殊回调功能将与 UI 相关的消息传递给 IDE。 帮助程序 UI 有助于与 IDE 进行更无缝的集成（通常使用**高级**按钮），从而提供更统一的最终用户体验。

 源代码管理插件不能对[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]shell 进行更改，因此无法更改源代码管理适配器包或 IDE 提供的源代码管理 UI。 它必须最大限度地利用通过实现各种源代码管理插件 API 功能提供的灵活性，这些功能有助于最终用户获得集成体验。 源代码管理插件 API 文档的参考部分包括某些高级源代码管理插件功能的信息。 要利用这些功能，源代码管理插件必须在初始化期间将其高级功能声明给 IDE，并且必须为每个功能实现特定的高级功能。

## <a name="see-also"></a>请参阅
- [源代码管理插件](../../extensibility/source-control-plug-ins.md)
- [术语表](../../extensibility/source-control-plug-in-glossary.md)
- [创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)
