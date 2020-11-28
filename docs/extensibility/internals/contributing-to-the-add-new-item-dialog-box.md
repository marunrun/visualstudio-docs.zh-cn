---
title: 参与 "添加新项" 对话框 |Microsoft Docs
description: 在 Visual Studio 中，通过在项目注册表子项下注册添加项模板来了解如何参与 "添加新项" 对话框。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 94a13890f0b5e60b1da204b89a01c1cadc6d00c4
ms.sourcegitcommit: 2244665d5a0e22d12dd976417f2a782e68684705
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2020
ms.locfileid: "96304631"
---
# <a name="contribute-to-the-add-new-item-dialog-box"></a>参与 "添加新项" 对话框
项目子类型可以为 "**添加新项**" 对话框提供一个完整的新目录，方法是在 **项目** 注册表子项下注册 "**添加项** 模板"。

## <a name="register-add-new-item-templates"></a>注册 "添加新项" 模板
 此部分位于注册表中 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0\Projects** 下。 下面的注册表项假定 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 项目由假设项目子类型聚合。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]下面列出了项目的条目。

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

 **AddItemTemplates\TemplateDirs** 子项包含注册表项，其中包含指向 "**添加新项**" 对话框中可用项的目录的路径。

 环境会自动加载 **项目** 注册表子项下的所有 **AddItemTemplates** 数据。 此数据可以包含基本项目实现的数据，以及特定项目子类型类型的数据。 每个项目子类型都由项目类型 **GUID** 标识。 项目子类型可以指定应将一组其他的 **添加项** 模板用于特定的风格项目实例，方法是 `VSHPROPID_ AddItemTemplatesGuid` <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2> 在实现中支持枚举 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> ，以返回项目子类型的 GUID 值。 如果 `VSHPROPID_AddItemTemplatesGuid` 未指定该属性，则使用基本项目 GUID。

 您可以通过在 " **添加新项** " 对话框中实现 " <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg> 项目子类型" 聚合对象上的接口来筛选项。 例如，通过对项目进行聚合来实现数据库项目的项目子类型， [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 可以 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 通过实现筛选来从 " **添加新项** " 对话框中筛选特定项，进而可以通过支持中的来添加特定于数据库项目的项 `VSHPROPID_ AddItemTemplatesGuid` <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> 。 有关筛选和添加项到 " **添加新项** " 对话框的详细信息，请参阅将 [项添加到 "添加新项" 对话框](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)。

## <a name="see-also"></a>另请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>
- [通常用于扩展项目的对象的 Catid](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)
