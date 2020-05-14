---
title: 选项页的自动化支持 |微软文档
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
ms.openlocfilehash: fe45238948d5b4cdebbf9f002f6b242515e7622e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709936"
---
# <a name="automation-support-for-options-pages"></a>选项页的自动化支持
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] VSPackages 可以为 中的 **"工具**选项"菜单（**工具选项**页）提供自定义**选项**对话框，并可将其提供给自动化模型。

## <a name="tools-options-pages"></a>工具选项页
 要创建**工具选项**页，VSPackage 必须提供通过 VSPackage<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A>方法实现返回给环境的用户控件实现。 （或者，对于托管代码，<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A>该方法。

 允许通过自动化模型访问此新页面是可选的，但强烈建议。 您可以通过以下步骤执行此操作：

1. 通过实现<xref:EnvDTE._DTE.Properties%2A>IDispatch 派生的对象来扩展对象。

2. 将<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A>方法的实现（或对于托管代码<xref:Microsoft.VisualStudio.Shell.Package.GetAutomationObject%2A>的方法）返回到 IDispatch 派生的对象。

3. 当自动化使用者在自定义<xref:EnvDTE._DTE.Properties%2A>**Option**属性页上调用 该方法时，环境使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A>该方法获取自定义**工具选项**页的自动化实现。

4. 然后，VSPackage 的自动化对象用于提供 返回的每个<xref:EnvDTE.Property><xref:EnvDTE._DTE.Properties%2A>对象。

   有关实现自定义**工具选项**页的示例，请参阅[VSSDK 示例](https://github.com/Microsoft/VSSDK-Extensibility-Samples)。

## <a name="see-also"></a>请参阅
- [公开项目对象](../../extensibility/internals/exposing-project-objects.md)
