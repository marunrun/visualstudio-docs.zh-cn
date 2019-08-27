---
title: 字形控件 (源代码管理 VSPackage) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- glyphs, source control packages
- source control packages, glyphs
ms.assetid: b9413b08-b3c3-4fc3-a6e0-3dc0db3652d7
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b0960209b67c8d2f111296840119807d95bb2e2d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62538416"
---
# <a name="glyph-control-source-control-vspackage"></a>字形控件（源代码管理 VSPackage）
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

可用于源代码管理 Vspackage 的深度集成的一部分是能够显示其自己的标志符号，以指示源代码管理下的项的状态。  
  
## <a name="levels-of-glyph-control"></a>使用的标志符号控制级别  
 状态标志符号是一个图标，指示某个项时显示，例如，在的当前状态**解决方案资源管理器**中或在**类视图**。 源代码管理 VSPackage 可以运用两个级别的标志符号控件。 它可以限制所选的标志符号为一组预定义的标志符号提供[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]IDE，或者它可以定义一组自定义的标志符号显示。  
  
### <a name="default-set-of-glyphs"></a>默认的标志符号集  
 若要确定与中的项相关联的状态标志符号**解决方案资源管理器**，一个项目从使用源控件请求的状态标志符号<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2.GetSccGlyph%2A>。 源代码管理 VSPackage 可能会决定保留限制为与 IDE 提供的预定义标志符号的标志符号的选择。 在这种情况下，VSPackage 传递回表示 vsshell.idl 中定义的标志符号枚举的值的数组。 有关详细信息，请参阅<xref:Microsoft.VisualStudio.Shell.Interop.VsStateIcon>。这是一组预定义的设置的 IDE，例如"已签入"标志符号，和一个复选标记为"已签出"字形挂锁的标志符号。  
  
### <a name="custom-set-of-glyphs"></a>自定义设置的标志符号  
 源代码管理 VSPackage 时能够使用其自己的标志符号进行唯一的"外观和感觉"安装它。 当新的源代码管理 VSPackage 处于活动状态时，它应该能够开始使用其自己的标志符号即使在上一进行源代码管理 VSPackage 仍然加载，但处于非活动状态。 在此模式下，源代码管理 VSPackage 仍可以使用现有的图标以维护查看与一致[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]如果还选择能。  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>服务支持的接口， <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs>，利用它，可以选择实现 VSPackage，将通过 IDE 的要求。 当发出请求，时 IDE[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]反过来将尝试从当前已注册的源代码管理 VSPackage 中获取此接口。 如果接口存在于已注册 VSPackage，自定义标志符号的 IDE 的请求成功;否则为[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]IDE 使用其默认的标志符号集。  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs.GetCustomGlyphList%2A>方法由[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]为了获取一系列图像显示各种源代码管理状态。 源代码管理 VSPackage 对 IDE 返回其自定义标志符号的图像列表的句柄。 IDE 此时生成的图像列表的副本和更高版本使用它来选择要显示的标志符号。 如果不支持的新接口或`IVsSccGlyphs::GetCustomGlyphList`方法返回 E_NOTIMPL，然后在 IDE 获取其标志符号的标志符号提供的默认列表从[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs>   
 <xref:Microsoft.VisualStudio.Shell.Interop.VsStateIcon>   
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>
