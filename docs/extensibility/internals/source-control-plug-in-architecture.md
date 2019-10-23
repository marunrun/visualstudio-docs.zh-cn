---
title: 源代码管理插件体系结构 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, architecture
ms.assetid: 35351d4c-9414-409b-98fc-f2023e2426b7
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6f06f023a46fc9bc417e9630613a716f8dd448d2
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72723449"
---
# <a name="source-control-plug-in-architecture"></a>源代码管理插件体系结构
通过实现和附加源代码管理插件，你可以向 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 集成开发环境（IDE）添加源代码管理支持。 IDE 通过定义完善的源代码管理插件 API 连接到源代码管理插件。 IDE 通过提供由工具栏和菜单命令组成的用户界面（UI），公开源代码管理系统的版本控制功能。 源代码管理插件实现源代码管理功能。

## <a name="source-control-plug-in-resources"></a>源代码管理插件资源
 源代码管理插件提供了一些资源，可帮助创建版本控制应用程序并将其连接到 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE。 源代码管理插件包含必须由源代码管理插件实现的 API 规范，以便可以将其集成到 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE 中。 它还包含一个代码示例（编写在C++中），该示例实现一个框架源代码管理插件，该插件演示实现符合源代码管理插件 API 的基本函数的实现。

 源代码管理插件 API 规范可让你利用所选的任何源代码管理系统，前提是使用根据源代码管理插件 API 实现的所需函数集创建源代码管理 DLL。

## <a name="components"></a>组件数
 关系图中的源代码管理适配器包是 IDE 的组件，它将用户对源代码管理操作的请求转换为源代码管理插件支持的函数调用。 为此，IDE 和源代码管理插件必须有一个有效的对话框，该对话框在 IDE 和插件之间来回传递信息。 要使此对话框发生，它们必须使用相同的语言。 本文档中概述的源代码管理插件 API 是此交换的常见词汇。

 ![源代码管理体系结构关系图](../../extensibility/internals/media/vs_sccsdk_plug_in_arch.gif "vs_sccsdk_plug_in_arch")显示 VS 与源代码管理插件之间交互的体系结构关系图

 如体系结构关系图中所示，在关系图中标记为 VS shell 的 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] shell 承载用户的工作项目和关联的组件，如编辑器和解决方案资源管理器。 源代码管理适配器包处理 IDE 和源代码管理插件之间的交互。 源代码管理适配器包提供自己的源代码管理 UI。 它是用户与之交互的顶级 UI，以便启动和定义源代码管理操作的作用域。

 源代码管理插件可以有自己的 UI，它可能由两个部分组成，如图中所示。 标记为 "供应商 UI" 的框表示作为源代码管理插件创建者提供的自定义用户界面元素。 当用户调用高级源代码管理操作时，这些控件将由源代码管理插件直接显示。 标记为 "帮助 UI" 的框是一组通过 IDE 间接调用的源代码管理插件 UI 功能。 源代码管理插件通过 IDE 提供的特殊回调函数将与 UI 相关的消息传递到 IDE。 帮助器 UI 使与 IDE 更无缝地集成（通常通过使用 "**高级**" 按钮），从而提供更统一的最终用户体验。

 源代码管理插件不能对 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] shell 进行更改，因此不能对 IDE 提供的源代码管理适配器包或源代码管理用户界面进行更改。 它必须充分利用为最终用户提供集成体验的各种源代码管理插件 API 函数实现提供的灵活性。 源代码管理插件 API 文档的 "参考" 部分包含一些高级源代码管理插件功能的信息。 若要利用这些功能，源代码管理插件必须在初始化期间向 IDE 声明其高级功能，并且必须为每个功能实现特定的高级功能。

## <a name="see-also"></a>请参阅
- [源代码管理插件](../../extensibility/source-control-plug-ins.md)
- [术语表](../../extensibility/source-control-plug-in-glossary.md)
- [创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)