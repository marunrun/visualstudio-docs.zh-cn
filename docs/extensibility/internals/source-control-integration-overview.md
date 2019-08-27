---
title: 源控件集成概述 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], about source control
ms.assetid: 3a46e4eb-e677-49c3-8647-d927d035a19a
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9dd54872325766b432af7e3104e7ab9f431b79d7
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66322511"
---
# <a name="source-control-integration-overview"></a>源代码管理集成概述
本部分将进行比较的两种方法来将集成到 Visual Studio 源代码管理;源代码管理插件并提供了源代码管理解决方案，并突出显示新的源代码管理功能的 VSPackage。 Visual Studio 支持源代码管理 Vspackage 和源代码控制插件之间手动切换，以及自动基于解决方案的切换。

## <a name="source-control-integration"></a>源代码管理集成
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 支持两种类型的源代码管理集成选项。 在所有版本的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]，仍可以集成基于源控制插件 API （以前也称为 MSSCCI API），它使用 Visual Studio 源控件用户界面 （同时提供基本的源代码管理功能的插件UI)。 源代码管理 VSPackage，但是，提供了新的深度集成[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]路径适用于需要高级别的复杂程度和自主性在其源控件模型中的源代码管理集成。

 ![源控件概述](../../extensibility/internals/media/sourcectnrloverview.gif "SourceCtnrlOverview")

## <a name="source-control-plug-in"></a>源代码管理插件
 所有版本的 Visual Studio 都支持集成路径作为源控制插件 API 规范 1.2 版。 源控件插件实施者写入实现进行源代码管理集成和注册的源控制插件 API 函数，如中所述的 DLL[创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)。 在这种方法，集成开发环境 (IDE) 使用[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]UI 对话框，如签入签出、 工具/选项属性页、 工具栏和源控件标志符号。 严格遵守源控制插件 API 也可确保轻松集成到 Visual Studio 和用户提供可靠的体验。 这意味着，源代码管理插件必须实现的功能和详细的 API 中的回调的大多数。

 若要实现源代码管理插件使用源控制插件 API，请执行以下步骤：

1. 创建实现中所指定的函数的 DLL[源代码管理插件](../../extensibility/source-control-plug-ins.md)。

2. 相应的注册表项，从而注册该 DLL (中所述[如何：安装源代码管理插件](../../extensibility/internals/how-to-install-a-source-control-plug-in.md))。

3. 创建一个帮助程序 UI 和显示当出现提示时源代码管理适配器包 （处理通过源代码管理插件的源代码管理功能的 Visual Studio 组件）

   一个源代码管理命令响应，Visual Studio IDE 提供了一个标准用户界面的基本操作，然后将信息传递到源代码管理插件通过源控件插件 API 中定义的函数。 有关高级选项，源代码管理插件不能对调用以提供自己的 UI，例如，浏览源代码管理的项目。 这意味着，用户可能会出现两种可能具有不同样式的 UI 时面对的源代码管理： Visual Studio 会显示在 UI 和源代码管理插件显示用户界面。 这是最明显与高级的源代码管理操作。

### <a name="drawbacks-to-implementing-a-source-control-plug-in"></a>实现源代码管理插件的缺点

- 有关高级功能，用户可能会看到两种不同样式的接口，从而导致可能的混淆。

- 源代码管理插件仅限于权限隐含的源控制插件 API 的源控件模型。

- 源控件插件 API 可能太多限制的一些源代码管理方案。

### <a name="advantages-to-implementing-a-source-control-plug-in"></a>实现源代码管理插件的优点

- Visual Studio 提供所有基本源代码管理操作的所有用户的界面，以便源代码管理插件不需要实现潜在的复杂 UI。

- 由于严格的 API，源代码管理插件随时可与外部源控制计划，以提供更广泛的功能; 交互Visual Studio 并不关心过得多的源代码管理功能如何完成，仅，根据源控制插件 API 来完成。

- 它是更轻松地实现了源代码管理插件与源代码管理 VSPackage。

## <a name="source-control-vspackage"></a>源代码管理 VSPackage
 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 允许深度集成到 Visual Studio 中使用源代码管理功能的完全控制和提供 Visual Studio 源代码管理用户界面的完全替换。 源代码管理 VSPackage Visual Studio 注册，并且提供了源代码管理功能。 尽管可以使用 Visual Studio 注册多个源代码管理 Vspackage，只有一个可以处于活动状态一次。 源代码管理 VSPackage 处于活动状态时，Visual Studio 中具有完全控制的源代码管理功能和外观。 所有其他源代码管理 Vspackage 可能会在系统中注册处于非活动状态，并将不显示任何 UI。

 实现源代码管理 VSPackage 需要一个"全或无"的策略。 源代码管理 VSPackage 的创建者必须投入大量精力实现大量源控件接口和新 UI 元素 （对话框、 菜单和工具栏） 以涵盖整个源控制功能。 请参阅[创建源代码管理 VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md)的更多详细信息。

### <a name="drawbacks-to-implementing-a-source-control-vspackage"></a>实现源代码管理 VSPackage 的缺点

- VSPackage 必须实现多个复杂的接口，以与 Visual Studio 成功集成。

- VSPackage 必须提供所需的源控件，则所有用户界面Visual Studio 将提供此区域中的提供任何帮助。

- 源代码管理 VSPackage 联系紧密绑定到 Visual Studio 并不能执行操作的独立程序，因此不能与源代码管理程序的外部版本一样轻松地共享功能。

### <a name="advantages-to-implementing-a-source-control-vspackage"></a>实现源代码管理 VSPackage 的优点

- 因为 VSPackage 具有完全控制源代码管理 UI 和功能，则用户会看到适合源代码管理的无缝界面。

- VSPackage 不局限于特定的源控件模型。

## <a name="see-also"></a>请参阅
- [源代码管理](../../extensibility/internals/source-control.md)
- [创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)
- [创建源代码管理 VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md)
- [源代码管理中的新增功能](../../extensibility/internals/what-s-new-in-source-control.md)