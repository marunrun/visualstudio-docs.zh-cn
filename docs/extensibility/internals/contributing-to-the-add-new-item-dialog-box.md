---
title: 参与到添加新建项对话框 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Add New Item dialog box, contributing to
ms.assetid: b2e53175-9372-4d17-8c2b-9264c9e51e9c
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 443f52edda5f3bedb2e3f8c8dbbe748254fd7be7
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66335573"
---
# <a name="contribute-to-the-add-new-item-dialog-box"></a>贡献添加新项对话框
项目子类型可以提供完整的项的新目录**添加新项**对话框中的注册**添加项**下的模板**项目**注册表子项。

## <a name="register-add-new-item-templates"></a>注册添加新项模板
 本部分位于**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0\Projects**注册表中。 下面的注册表项假定[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]项目假设项目子类型进行聚合。 为项[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]下面列出了项目。

```
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0\Projects\{F184B08F-C81C-45F6-A57F-5ABD9991F28F}]
@="#2143"
"DefaultProjectExtension"="vbproj"
"PossibleProjectExtensions"="vbproj;vbp"
"ProjectTemplatesDir"="visualStudioInstallPath\\Vb\\.\\VBProjects"

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0\Projects\{F184B08F-C81C-45F6-A57F-5ABD9991F28F}\AddItemTemplates\TemplateDirs\{12345678-1234-1234-1122334455667788}\/1]
@="#100"
"TemplatesDir"="projectSubTypeTemplatesDir\\VBProjectItems"
```

 **AddItemTemplates\TemplateDirs**子项包含与项所做中可用的目录的路径的注册表条目**添加新项**放置对话框。

 环境会自动加载的所有**AddItemTemplates**下的数据**项目**注册表子项。 此数据可以包括基础项目实现的数据以及特定项目子类型类型数据。 每个项目子类型由项目类型**GUID**。 项目子类型可以指定的设置备用**添加项**模板应该用于通过支持的特定风格的项目实例`VSHPROPID_ AddItemTemplatesGuid`来自枚举<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2>中<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>要返回的项目子类型的 GUID 值实现。 如果`VSHPROPID_AddItemTemplatesGuid`未指定属性，使用 GUID 的基础项目。

 您可以筛选中的项**添加新项**对话框中，通过实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg>项目子类型聚合器对象上的接口。 例如，通过聚合来实现数据库项目的项目子类型才能[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]项目中，可以筛选[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]中的特定于项**添加新项**通过实现筛选，然后在对话框打开，可以添加通过支持数据库特定于项目的项`VSHPROPID_ AddItemTemplatesGuid`在<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>。 有关详细信息筛选和添加的项**添加新项**对话框中，请参阅[将项添加到添加新项对话框中](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>
- [对象通常用于扩展项目的 Catid](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)