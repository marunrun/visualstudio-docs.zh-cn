---
title: 为 VS 包提供自动化 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, automation [Visual Studio SDK]
- automation [Visual Studio SDK], VSPackages
ms.assetid: 104c4c55-78b8-42f4-b6b0-9a334101aaea
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6364f9cbaf3409e076eeb77365e5d793c7be96cb
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705953"
---
# <a name="providing-automation-for-vspackages"></a>提供适用于 VSPackage 的自动化
提供 VSPackage 自动化的两种主要方法：通过实现特定于 VSPackage 的对象和实现标准自动化对象。 通常，这些用于扩展环境的自动化模型。

## <a name="vspackage-specific-objects"></a>VS 包特定对象
 自动化模型中的某些位置要求您提供 VSPackage 独有的自动化对象。 例如，新项目需要仅提供 VSPackage 的不同对象。 这些对象的名称在注册表中输入，并通过对环境`DTE`对象的调用获得。

 当自动化使用者使用通过标准对象的 Object 属性提供的对象时，也可以获取特定于 VSPackage 的对象。 例如，标准`Window`对象具有一个`Object`属性，通常称为 属性。 `Windows.Object` 当使用者调用`Window.Object`VSPackage 中实现的窗口时，将传递自己设计的特定自动化对象。

#### <a name="projects"></a>项目
 VSPackage 可以通过自己的 VSPackage 特定对象扩展新项目类型的自动化模型。 为 VSPackage 提供新的自动化对象的主要目的是将唯一<xref:Microsoft.VisualStudio.VCProjectEngine.VCProject><xref:VSLangProj80.VSProject2>项目对象与 对象区分开来。 当您希望提供一种从其他项目类型中并排显示的项目类型以外的单一或迭代项目类型的方法时，这种差别化是很方便的。 有关详细信息，请参阅[公开项目对象](../../extensibility/internals/exposing-project-objects.md)。

#### <a name="events"></a>事件
 环境的事件体系结构为您提供了另一个位置来追加自己的 VSPackage 特定对象。 例如，通过创建自己的唯一事件对象，可以扩展环境的事件模型。 当新项目添加到您自己的项目类型时，您可能希望提供您自己的事件。 有关详细信息，请参阅[公开事件](../../extensibility/internals/exposing-events-in-the-visual-studio-sdk.md)。

#### <a name="window-objects"></a>窗口对象
 Windows 可以在调用时将特定于 VSPackage 的自动化对象传回环境。 实现派生自<xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject>的对象<xref:EnvDTE.IExtensibleObject>或`IDispatch`该回手属性，扩展其驻点的窗口对象。 例如，可以使用此方法为窗口框架中设置的控件提供自动化。 此对象及其可能扩展的任何其他对象的语义是您设计的。 有关详细信息，请参阅[如何：为 Windows 提供自动化](../../extensibility/internals/how-to-provide-automation-for-windows.md)。

#### <a name="options-pages-on-the-tools-menu"></a>"工具"菜单上的选项页面
 您可以通过实现页面和向注册表添加信息来创建页面来扩展工具、选项自动化模型，以创建您自己的选项。 然后，可以通过环境对象模型与任何其他选项页一样调用您的页面。 如果通过 VSPackages 添加到环境的功能的设计需要选项页，则还应添加自动化支持。 有关详细信息，请参阅[选项页的自动化支持](../../extensibility/internals/automation-support-for-options-pages.md)。

## <a name="standard-automation-objects"></a>标准自动化对象
 要扩展项目的自动化，您还可以实现标准自动化对象（派生自`IDispatch`），该对象位于其他项目对象旁边，并实现标准方法和属性。 标准对象`Projects`的示例包括插入到解决方案层次结构（如 、`Project`和`ProjectItem``ProjectItems`） 的项目对象。 每个新项目类型都应实现这些对象（可能还有其他对象，具体取决于项目的语义）。

 从某种意义上说，这些对象提供了 VSPackage 特定项目对象的相反优势。 标准自动化对象允许以通用方式使用项目，就像支持相同对象的任何其他项目一样。 因此，针对常规`Project`和`ProjectItem`对象编写的外接程序可以针对任何类型的项目运行。 有关详细信息，请参阅[项目建模](../../extensibility/internals/project-modeling.md)。
