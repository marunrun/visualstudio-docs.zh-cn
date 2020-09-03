---
title: " (源代码管理的标志符号控件 VSPackage) |Microsoft Docs"
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- glyphs, source control packages
- source control packages, glyphs
ms.assetid: b9413b08-b3c3-4fc3-a6e0-3dc0db3652d7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9db1b4542eae293e39cda674fac3eb984aa77d3e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80708320"
---
# <a name="glyph-control-source-control-vspackage"></a> (源代码管理的标志符号控件 VSPackage) 
可用于源代码管理的深度集成 Vspackage 是显示自己的标志符号，以指示源代码管理下项的状态的能力。

## <a name="levels-of-glyph-control"></a>字形控件的级别
 状态标志符号是一个图标，指示项在显示时的当前状态，例如在 **解决方案资源管理器** 或 **类视图**中。 源代码管理 VSPackage 可以执行两个级别的字形控件。 它可以将字形选择限制为 IDE 提供的一组预定义字形 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ，或者可以定义要显示的一组自定义字形。

### <a name="default-set-of-glyphs"></a>默认字型集
 若要确定与 **解决方案资源管理器**中的项关联的状态标志符号，项目将使用从源代码管理请求状态标志符号 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2.GetSccGlyph%2A> 。 源代码管理 VSPackage 可能决定保留仅限于 IDE 提供的预定义字形的字形选择。 在这种情况下，VSPackage 会传递返回值的数组，这些值表示在 *vsshell*中定义的标志符号枚举。 有关详细信息，请参阅 <xref:Microsoft.VisualStudio.Shell.Interop.VsStateIcon>。 这是由 IDE 设置的一组预定义字形，如检入标志符号的挂锁和检出标志符号的复选标记。

### <a name="custom-set-of-glyphs"></a>自定义字形集
 源代码管理 VSPackage 可以使用自己的标志符号，在安装时具有独特的外观。 当新的源代码管理 VSPackage 处于活动状态时，它应该能够开始使用自己的标志符号，即使之前的源代码管理 VSPackage 仍处于加载状态，但仍处于非活动状态。 在此模式下，源控件 VSPackage 仍可使用现有的图标，以便在其选择时保持一致的外观 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

 该 <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager> 服务支持一个接口， <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs> VSPackage 可以选择实现此接口，并将由 IDE 请求。 当 IDE 发出请求时， [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 将转而尝试从当前注册的源控件 VSPackage 获取此接口。 如果注册的 VSPackage 中存在该接口，则 IDE 对自定义标志符号的请求将成功;否则， [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE 将使用其默认的字形集。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs.GetCustomGlyphList%2A>使用方法 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 来获取显示各种源代码管理状态的图像列表。 源代码管理 VSPackage 返回到 IDE，其自定义标志符号的图像列表的句柄。 此时，IDE 将创建图像列表的副本，并在以后使用它来选择要显示的标志符号。 如果不支持新接口或 `IVsSccGlyphs::GetCustomGlyphList` 方法返回 `E_NOTIMPL` ，则 IDE 将从提供的标志符号的默认列表中获取其标志符号 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs>
- <xref:Microsoft.VisualStudio.Shell.Interop.VsStateIcon>
- <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>
