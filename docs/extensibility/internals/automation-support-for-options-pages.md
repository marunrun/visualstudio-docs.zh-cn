---
title: "\"选项\" 页的自动化支持 |Microsoft Docs"
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Tools Options pages [Visual Studio SDK], automation support
- automation [Visual Studio SDK], creating Tools Options pages
ms.assetid: 0b25b82c-7432-4e0a-9e84-350269ba8260
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 03360bfc01110e7b4ef73956f0199aaaed9cee2c
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75848972"
---
# <a name="automation-support-for-options-pages"></a>"选项" 页的自动化支持
Vspackage 可以在 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 的 "**工具**" 菜单中提供自定义**选项**对话框（"**工具选项**" 页），并使它们可用于自动化模型。

## <a name="tools-options-pages"></a>工具选项页
 若要创建 "**工具选项**" 页，VSPackage 必须通过 VSPackage 的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A> 方法实现来提供向环境返回的用户控件实现。 （对于托管代码，则为 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A> 方法。）

 这是可选的，但强烈建议您通过自动化模型允许访问此新页。 为此，可以执行以下步骤：

1. 通过实现 IDispatch 派生对象扩展 <xref:EnvDTE._DTE.Properties%2A> 对象。

2. 返回 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> 方法的实现（对于托管代码，则返回派生对象的 <xref:Microsoft.VisualStudio.Shell.Package.GetAutomationObject%2A> 方法）。

3. 当自动化使用者在自定义**选项**属性页上调用 <xref:EnvDTE._DTE.Properties%2A> 方法时，环境使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> 方法来获取自定义**工具选项**页的自动化实现。

4. 然后，使用 VSPackage 的自动化对象提供 <xref:EnvDTE._DTE.Properties%2A>返回的每个 <xref:EnvDTE.Property>。

   有关实现自定义**工具选项**页的示例，请参阅[VSSDK 示例](https://github.com/Microsoft/VSSDK-Extensibility-Samples)。

## <a name="see-also"></a>另请参阅
- [公开项目对象](../../extensibility/internals/exposing-project-objects.md)
