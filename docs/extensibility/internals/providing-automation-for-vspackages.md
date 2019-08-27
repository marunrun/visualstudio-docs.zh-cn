---
title: 提供 Vspackage 的自动化 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, automation [Visual Studio SDK]
- automation [Visual Studio SDK], VSPackages
ms.assetid: 104c4c55-78b8-42f4-b6b0-9a334101aaea
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9685d14651a40fd26842e0d922fefbc0075c00c5
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66341485"
---
# <a name="providing-automation-for-vspackages"></a>提供适用于 VSPackage 的自动化
有两种主要方法来提供你的 Vspackage 的自动化： 通过实现特定于 VSPackage 的对象以及通过实现标准自动化对象。 通常情况下，这些一起用于扩展自动化模型的环境。

## <a name="vspackage-specific-objects"></a>特定于 VSPackage 的对象
 自动化模型中的某些地方要求你提供专为你的 VSPackage 的自动化对象。 例如，新的项目需要你的 VSPackage 提供的不同对象。 这些对象的名称在注册表中输入，并通过调用环境获得`DTE`对象。

 自动化使用者使用通过标准的对象的对象属性提供的对象时，还可以获取特定于 VSPackage 的对象。 例如，标准`Window`对象具有`Object`属性，通常称为`Windows.Object`属性。 当使用者调用`Window.Object`上一个窗口，在你的 VSPackage 中实现，您传递回自己设计的一个特定的自动化对象。

#### <a name="projects"></a>项目
 Vspackage 可以扩展自动化模型的新的项目类型通过其自己特定于 VSPackage 的对象。 从对象提供新的自动化对象，为你的 VSPackage 来区分你唯一的项目的主要目的<xref:Microsoft.VisualStudio.VCProjectEngine.VCProject>或<xref:VSLangProj80.VSProject2>对象。 此区别是非常方便你想要提供一种方法来挑选出或循环访问您的其他项目类型，除了项目的类型应显示同时在解决方案中。 有关详细信息，请参阅[公开项目对象](../../extensibility/internals/exposing-project-objects.md)。

#### <a name="events"></a>事件
 环境的事件体系结构提供了可追加您自己的特定于 VSPackage 的对象的另一个位置。 例如，通过创建您自己的唯一事件的对象，可以扩展项目的环境的事件模型。 您可能想要提供自己的新项添加到项目类型时的事件。 有关详细信息，请参阅[公开事件](../../extensibility/internals/exposing-events-in-the-visual-studio-sdk.md)。

#### <a name="window-objects"></a>窗口对象
 Windows 可以传递回特定于 VSPackage 的自动化对象返回给调用时环境。 实现派生自的对象<xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject>，<xref:EnvDTE.IExtensibleObject>或`IDispatch`，将返回传递属性，扩展在其中确定位置的窗口对象。 例如，这种方法可用于提供在窗口框架中放置的控件的自动化。 此对象以及它可能会延长的任何其他对象的语义是由您负责进行设计。 有关详细信息，请参阅[如何：提供适用于 Windows 的自动化](../../extensibility/internals/how-to-provide-automation-for-windows.md)。

#### <a name="options-pages-on-the-tools-menu"></a>在工具菜单上的选项页
 可以创建页以扩展工具选项自动化模型通过实现页面并将信息添加到注册表，以创建你自己的选项。 然后，可以像任何其他选项页的环境对象模型调用您的页面。 如果要添加到 Vspackage 通过环境的功能的设计需要选项页，则应添加的自动化支持。 有关详细信息，请参阅[选项页的自动化支持](../../extensibility/internals/automation-support-for-options-pages.md)。

## <a name="standard-automation-objects"></a>标准自动化对象
 若要扩展的项目的自动化，你还实施标准自动化对象 (派生自`IDispatch`) 的其他项目对象旁边构建并实现标准方法和属性。 标准的对象的示例包括如插入到解决方案层次结构的项目对象`Projects`， `Project`， `ProjectItem`，和`ProjectItems`。 每个新的项目类型应实现这些对象，则可能你的项目的其他的具体取决于语义）。

 在某种意义上，这些对象提供特定于 VSPackage 的项目对象的另一优势。 标准自动化对象允许你的项目以使用支持的相同对象的其他任何项目一样的通用方式。 因此外, 接程序，针对常规编写`Project`和`ProjectItem`对象端可针对任何类型的项目。 有关详细信息，请参阅[项目建模](../../extensibility/internals/project-modeling.md)。