---
title: "\"选项\" 页的自动化支持 |Microsoft Docs"
description: 了解如何使 Vspackage 中的自定义工具选项页可用于 Visual Studio 自动化模型。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Tools Options pages [Visual Studio SDK], automation support
- automation [Visual Studio SDK], creating Tools Options pages
ms.assetid: 0b25b82c-7432-4e0a-9e84-350269ba8260
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1e15b1f8bdd27e013e1ef2060d9867a81e8ddde3
ms.sourcegitcommit: b1b747063ce0bba63ad2558fa521b823f952ab51
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/26/2020
ms.locfileid: "96190026"
---
# <a name="automation-support-for-options-pages"></a>"选项" 页的自动化支持
Vspackage 可以) 中的 "**工具**" 菜单 ("工具"**选项** 页提供自定义 **选项** 对话框 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ，并使它们可用于自动化模型。

## <a name="tools-options-pages"></a>工具选项页
 若要创建 " **工具选项** " 页，VSPackage 必须通过该方法的 VSPackage 实现来提供向环境返回的用户控件实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A> 。  (或，对于托管代码，则为 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A> 方法。 ) 

 这是可选的，但强烈建议您通过自动化模型允许访问此新页。 可通过以下步骤执行此操作：

1. <xref:EnvDTE._DTE.Properties%2A>通过实现 IDispatch 派生对象来扩展对象。

2. 返回 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> (或托管代码的方法的实现， <xref:Microsoft.VisualStudio.Shell.Package.GetAutomationObject%2A> 方法) 到 IDispatch 派生的对象。

3. 当自动化使用者 <xref:EnvDTE._DTE.Properties%2A> 在自定义 **选项** 属性页上调用方法时，环境将使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> 方法来获取自定义 " **工具选项** " 页的自动化实现。

4. 然后，将使用 VSPackage 的自动化对象来提供返回的每个对象 <xref:EnvDTE.Property> <xref:EnvDTE._DTE.Properties%2A> 。

   有关实现自定义 **工具选项** 页的示例，请参阅 [VSSDK 示例](https://github.com/Microsoft/VSSDK-Extensibility-Samples)。

## <a name="see-also"></a>请参阅
- [公开项目对象](../../extensibility/internals/exposing-project-objects.md)
