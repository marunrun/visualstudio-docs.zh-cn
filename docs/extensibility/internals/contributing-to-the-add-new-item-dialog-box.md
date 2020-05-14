---
title: 向"添加新项目"对话框投稿 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Add New Item dialog box, contributing to
ms.assetid: b2e53175-9372-4d17-8c2b-9264c9e51e9c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 83444d9be6ba23392b792a0187bf46dc9920c465
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709279"
---
# <a name="contribute-to-the-add-new-item-dialog-box"></a>参与"添加新项目"对话框
项目子类型可以通过在**项目**注册表子键下注册 **"添加项目"** 模板，为"**添加新项目"** 对话框提供完整的项目新目录。

## <a name="register-add-new-item-templates"></a>注册添加新项目模板
 此部分位于**HKEY_LOCAL_MACHINE_SOFTWARE_Microsoft_VisualStudio_8.0\注册表中的项目**下。 下面的注册表项假定由假设[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]的项目子类型聚合的项目。 项目条目[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]如下。

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

 **AddItemTemplates_TemplateDirs**子键包含注册表项，其中包含目录的路径，其中放置了"**添加新项目"** 对话框中提供的项。

 环境在**项目**注册表子键下自动加载所有**AddItemTemplates**数据。 此数据可以包括基础项目实现的数据以及特定项目子类型类型的数据。 每个项目子类型由项目类型**GUID**标识。 项目子类型可以指定一组备用的**Add Item**模板应用于特定调味品项目实例，通过支持实现`VSHPROPID_ AddItemTemplatesGuid`中的<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2><xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>枚举来返回项目子类型的 GUID 值。 如果未指定`VSHPROPID_AddItemTemplatesGuid`该属性，则使用基础项目 GUID。

 您可以通过在项目子类型聚合器对象上实现接口来<xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg>筛选"**添加新项目"** 对话框中的项。 例如，通过[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]聚合项目来实现数据库项目的项目子类型可以通过实现筛选来筛选"**添加新项目"** 对话框中`VSHPROPID_ AddItemTemplatesGuid`<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]的特定项，进而可以通过 在 中支持添加数据库项目特定的项。 有关筛选项目并将项目添加到"**添加新项目"** 对话框的详细信息，请参阅[将项添加到"添加新项目"对话框](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>
- [通常用于扩展项目的对象的 CATID](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)
