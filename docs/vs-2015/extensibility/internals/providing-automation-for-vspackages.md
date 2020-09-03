---
title: 为 Vspackage 提供自动化 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, automation [Visual Studio SDK]
- automation [Visual Studio SDK], VSPackages
ms.assetid: 104c4c55-78b8-42f4-b6b0-9a334101aaea
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c6eb76eba76567f2966323d4058c9e752cb6fb69
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68200972"
---
# <a name="providing-automation-for-vspackages"></a>提供适用于 VSPackage 的自动化
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

可通过两种主要方式为 Vspackage 提供自动化：通过实现 VSPackage 特定的对象并实现标准自动化对象。 通常，它们一起用于扩展环境的自动化模型。  
  
## <a name="vspackage-specific-objects"></a>特定于 VSPackage 的对象  
 自动化模型中的某些位置需要提供 VSPackage 独有的自动化对象。 例如，新项目需要只有你的 VSPackage 提供的不同对象。 这些对象的名称是在注册表中输入的，并通过调用环境对象来获取 `DTE` 。  
  
 当自动化使用者使用通过标准对象的对象属性提供的对象时，也可以获取 VSPackage 特定的对象。 例如，标准 `Window` 对象有一个 `Object` 属性，该属性通常称为 `Windows.Object` 属性。 当使用者在 `Window.Object` VSPackage 中实现的窗口上调用时，会将自己的特定自动化对象传递回自己的设计。  
  
#### <a name="projects"></a>项目  
 Vspackage 可以通过其自己的 VSPackage 特定对象扩展新项目类型的自动化模型。 为 VSPackage 提供新的自动化对象的主要目的是将您的唯一项目对象与 <xref:Microsoft.VisualStudio.VCProjectEngine.VCProject> 或对象区分开来 <xref:VSLangProj80.VSProject2> 。 当你想要提供一种方法来使你的项目类型与其他项目类型分离或循环访问时，如果它们在解决方案中并行出现，则可以使用这种区别。 有关详细信息，请参阅 [公开项目对象](../../extensibility/internals/exposing-project-objects.md)。  
  
#### <a name="events"></a>事件  
 环境的事件体系结构提供了一个用于附加自己的 VSPackage 特定对象的其他位置。 例如，通过创建您自己的唯一事件对象，您可以扩展该环境的项目的事件模型。 将新项添加到自己的项目类型时，可能需要提供自己的事件。 有关详细信息，请参阅 [公开事件](../../extensibility/internals/exposing-events-in-the-visual-studio-sdk.md)。  
  
#### <a name="window-objects"></a>窗口对象  
 调用时，Windows 可以将 VSPackage 特定的自动化对象传回环境。 您可以实现一个派生自的对象 <xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibleObject> ， <xref:EnvDTE.IExtensibleObject> 或者执行 `IDispatch` 返回属性的对象，扩展该对象所在的窗口对象。 例如，您可以使用此方法为窗口框架中的控件提供自动化。 此对象以及它可能扩展的任何其他对象的语义是您要设计的。 有关详细信息，请参阅 [如何：为 Windows 提供自动化](../../extensibility/internals/how-to-provide-automation-for-windows.md)。  
  
#### <a name="options-pages-on-the-tools-menu"></a>"工具" 菜单上的 "选项" 页  
 可以通过实现页面并将信息添加到注册表来创建扩展工具、选项自动化模型的页面，以创建自己的选项。 然后，可以通过环境对象模型（与任何其他选项页）调用页。 如果通过 Vspackage 添加到环境中的功能的设计需要选项页，则还应添加自动化支持。 有关详细信息，请参阅 " [自动支持选项" 页](../../extensibility/internals/automation-support-for-options-pages.md)。  
  
## <a name="standard-automation-objects"></a>标准自动化对象  
 若要扩展项目的自动化，还可以实现 (派生自 `IDispatch` 其他项目对象旁的) 的标准自动化对象并实现标准方法和属性。 标准对象的示例包括插入到解决方案层次结构中的项目对象 `Projects` ，例如、、 `Project` `ProjectItem` 和 `ProjectItems` 。 每个新项目类型都应根据项目) 的语义 (和其他对象实现这些对象。  
  
 从某种意义上讲，这些对象提供 VSPackage 特定的项目对象的另一个优点。 标准自动化对象允许以一般化方式使用项目，如支持相同对象的任何其他项目。 因此，针对 "常规" 和 "对象" 编写的外接程序 `Project` `ProjectItem` 可以针对任何类型的项目运行。 有关详细信息，请参阅 [项目建模](../../extensibility/internals/project-modeling.md)。
