---
title: 源代码管理集成概述 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], about source control
ms.assetid: 3a46e4eb-e677-49c3-8647-d927d035a19a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d80363286f5f0cac9a5ceb2e8ac9d20345df9e6f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705122"
---
# <a name="source-control-integration-overview"></a>源代码管理集成概述
本节比较了集成到 Visual Studio 源代码管理中的两种方法;源控件插件和 VSPackage，提供源代码管理解决方案并突出显示新的源代码管理功能。 Visual Studio 允许在源代码管理 VS 包和源代码管理插件之间手动切换，以及基于解决方案的自动切换。

## <a name="source-control-integration"></a>源代码管理集成
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]支持两种类型的源代码管理集成选项。 在所有版本中[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]，您仍可以基于源代码管理插件 API（以前也称为 MSSCCI API）集成插件，该 API 在使用 Visual Studio 源代码管理用户界面 （UI） 时提供基本的源代码管理功能。 另一方面，源代码管理 VSPackage 提供了一种新的深度集成[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]路径，适用于源代码管理集成，需要源代码管理模型的高度复杂性和自主性。

 ![源代码管理概述](../../extensibility/internals/media/sourcectnrloverview.gif "源Ctnrl概述")

## <a name="source-control-plug-in"></a>源代码管理插件
 所有版本的 Visual Studio 都支持源代码管理插件 API 规范版本 1.2 作为集成路径。 源代码管理插件实现者编写一个 DLL，该 DLL 实现源代码管理插件 API 功能，用于源代码管理集成和注册，如[创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)中所述。 在此方法中，集成开发环境 （IDE） 使用[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]UI 用于对话框，例如签入、签出、工具/选项属性页、工具栏和源代码管理字形。 严格遵守源代码管理插件 API 可确保轻松集成到 Visual Studio 中，并为用户提供无故障体验。 这意味着源代码管理插件必须实现 API 中详述的大多数功能和回调。

 要使用源代码管理插件 API 实现源代码管理插件，请按照以下步骤操作：

1. 创建实现[源代码管理插件](../../extensibility/source-control-plug-ins.md)中指定的函数的 DLL。

2. 通过创建适当的注册表项注册 DLL（[在"如何：安装源代码管理插件"](../../extensibility/internals/how-to-install-a-source-control-plug-in.md)中所述）。

3. 创建帮助程序 UI 并在由源代码管理适配器包（通过源代码管理插件处理源代码管理功能的 Visual Studio 组件）提示时显示

   为了响应源代码管理命令，Visual Studio IDE 为基本操作提供了标准 UI，然后通过源代码管理插件 API 中定义的函数将信息传递给源代码管理插件。 对于高级选项，可以调用源代码管理插件来显示其自己的 UI，例如，浏览源代码管理的项目。 这意味着在处理源代码管理时，用户可能会看到两种可能不同的 UI 样式：Visual Studio 提供的 UI 和源代码管理插件提供的 UI。 这在高级源代码管理操作中最为明显。

### <a name="drawbacks-to-implementing-a-source-control-plug-in"></a>实现源代码管理插件的缺点

- 对于高级功能，用户可能会看到两种不同的接口样式，从而导致可能的混乱。

- 源代码管理插件仅限于源代码管理插件 API 隐含的源代码管理模型。

- 对于某些源代码管理方案，源代码管理插件 API 可能过于严格。

### <a name="advantages-to-implementing-a-source-control-plug-in"></a>实现源代码管理插件的优势

- Visual Studio 为所有基本源代码管理操作提供所有 UI，以便源代码管理插件不必实现潜在的复杂 UI。

- 由于 API 严格，源代码管理插件可以轻松地与外部源代码管理程序交互，以提供更广泛的功能;Visual Studio 不太关心源代码管理功能是如何实现的，只是它根据源代码管理插件 API 完成。

- 实现源代码管理插件比源代码管理 VSPackage 更容易。

## <a name="source-control-vspackage"></a>源代码管理 VS 包
 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]允许深度集成到 Visual Studio，全面控制源代码管理功能，并完全替换 Visual Studio 提供的源代码管理用户界面。 源代码管理 VSPackage 在 Visual Studio 注册并提供源代码管理功能。 尽管多个源代码管理 VSPackages 可以在 Visual Studio 中注册，但其中只有一个可以在任何时间处于活动状态。 源代码管理 VSPackage 在可视化工作室处于活动状态时可完全控制源代码管理功能和外观。 可能在系统中注册的所有其他源代码管理 VS 包处于非活动状态，不会显示任何 UI。

 实现源代码管理 VSPackage 需要"全无"策略。 源代码管理 VSPackage 的创建者必须投入大量精力来实现许多源代码管理接口和新的 UI 元素（对话框、菜单和工具栏），以涵盖整个源代码管理功能。 有关详细信息[，请参阅创建源代码管理 VS 包](../../extensibility/internals/creating-a-source-control-vspackage.md)。

### <a name="drawbacks-to-implementing-a-source-control-vspackage"></a>实现源代码管理 VS 包的缺点

- VSPackage 必须实现多个复杂的接口才能与 Visual Studio 成功集成。

- VS包必须提供源代码管理所需的所有 UI;视觉工作室将在此领域不提供任何帮助。

- 源代码管理 VSPackage 与 Visual Studio 紧密相连，无法使用独立程序运行，因此功能不能像源代码管理程序的外部版本那样容易共享。

### <a name="advantages-to-implementing-a-source-control-vspackage"></a>实现源代码管理 VS 包的优势

- 由于 VSPackage 可以完全控制源代码管理 UI 和功能，因此向用户提供了用于源代码控制的无缝界面。

- VSPackage 并不局限于特定的源代码管理模型。

## <a name="see-also"></a>请参阅
- [源代码管理](../../extensibility/internals/source-control.md)
- [创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)
- [创建源代码管理 VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md)
- [源代码管理中的新增功能](../../extensibility/internals/what-s-new-in-source-control.md)
