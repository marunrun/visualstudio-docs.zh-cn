---
title: 字形控制（源控制 VS 包） |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708320"
---
# <a name="glyph-control-source-control-vspackage"></a>字形控制（源控制 VS 包）
源代码管理 VSPackages 可用于的深度集成的一部分是能够显示自己的字形来指示源代码管理下的项的状态。

## <a name="levels-of-glyph-control"></a>字形控制级别
 状态字形是显示项目时指示项当前状态的图标，例如在**解决方案资源管理器**或**类视图中**。 源代码管理 VSPackage 可以执行两个级别的字形控制。 它可以将字形的选择限制为[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]IDE 提供的预定义的字形集，也可以定义要显示的自定义字形集。

### <a name="default-set-of-glyphs"></a>默认字形集
 要确定与**解决方案资源管理器**中的项关联的状态字形，项目使用 请求源控件中的状态字形<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2.GetSccGlyph%2A>。 源代码管理 VSPackage 可能决定将字形的选择限制为 IDE 提供的预定义字形。 在这种情况下，VSPackage 传递一个值数组，表示在*vsshell.idl*中定义的字形枚举。 有关详细信息，请参阅 <xref:Microsoft.VisualStudio.Shell.Interop.VsStateIcon>。 这是由 IDE 设置的预定义字形集，例如已签入字形的挂锁和签出字形的复选标记。

### <a name="custom-set-of-glyphs"></a>自定义字形集
 源代码管理 VSPackage 在安装时可以使用自己的字形来提供独特的外观。 当新的源代码管理 VSPackage 处于活动状态时，它应该能够开始使用自己的字形，即使以前的源代码管理 VSPackage 仍然加载但不活动。 在此模式下，源代码管理 VSPackage 仍可以使用现有图标，以便在选择[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]时保持与外观一致的外观。

 该服务<xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>支持一个接口，VS<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs>包可以选择实现该接口，IDE 会要求该接口。 当 IDE 发出请求时[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]，将尝试从当前注册的源代码管理 VSPackage 获取此接口。 如果接口存在于已注册的 VSPackage 中，则 IDE 的自定义字形请求将成功;如果该接口位于已注册的 VSPackage 中，则 IDE 对自定义字形的请求将成功;否则，IDE[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]将使用其默认的字形集。

 该方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs.GetCustomGlyphList%2A>用于[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]获取显示各种源代码管理状态的图像列表。 源控件 VSPackage 将自定义字形的句柄返回到映像列表的句柄。 IDE 此时会复制图像列表，然后使用它选择要显示的字形。 如果不支持新接口或`IVsSccGlyphs::GetCustomGlyphList`该方法返回`E_NOTIMPL`，则 IDE 将从 提供的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]字形的默认列表中获取其字形。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccGlyphs>
- <xref:Microsoft.VisualStudio.Shell.Interop.VsStateIcon>
- <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>
