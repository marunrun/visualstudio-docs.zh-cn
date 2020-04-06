---
title: 项目子类型 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], subtypes
- project subtypes [Visual Studio SDK]
ms.assetid: d235b47b-cf11-4d47-a63f-e33d9d16105d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 71dab4767c806b44cbd1f9638738b4a13d6b2bcb
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706409"
---
# <a name="project-subtypes"></a>项目子类型
项目子类型允许您自定义或调味[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]项目系统的行为。 自定义包括在项目文件中保存其他数据、在 **"添加新项目"** 对话框中添加或筛选项、控制程序集的调试和部署方式以及扩展项目**属性页**对话框。 VS包使用 COM 聚合实现项目子类型。

> [!NOTE]
> Visual C++项目系统不支持项目子类型。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]本身使用项目子类型来实现 SQL Server 和智能设备项目。

## <a name="in-this-section"></a>本节内容
- [项目子类型设计](../../extensibility/internals/project-subtypes-design.md)

 描述项目子类型的概念。

- [项目子类型的初始化序列](../../extensibility/internals/initialization-sequence-of-project-subtypes.md)

 描述按[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]环境划分的编程项目子类型初始化序列。

- [项目子类型扩展的属性和方法](../../extensibility/internals/properties-and-methods-extended-by-project-subtypes.md)

 提供使用项目子类型最常扩展的功能和方法的详细说明。

- [保留 MSBuild 项目文件中的数据](../../extensibility/internals/persisting-data-in-the-msbuild-project-file.md)

 描述如何在项目文件中保留数据，以及如何使用这些数据<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>跨项目子类型聚合级别维护项目文件中的数据。

- [项目属性用户界面](../../extensibility/internals/project-property-user-interface.md)

 描述项目子类型如何修改项目**属性页**对话框。

- [扩展基项目的对象模型](../../extensibility/internals/extending-the-object-model-of-the-base-project.md)

 提供有关项目子类型如何使用自动化扩展器扩展自动化对象模型的信息。

- [构成“添加新项”对话框](../../extensibility/internals/contributing-to-the-add-new-item-dialog-box.md)

 描述如何向"**添加新项目"对话框添加项**。

- [将数据保存在项目文件中](../../extensibility/saving-data-in-project-files.md)

 说明项目子类型如何使用托管包框架 （MPF） 在项目文件中保存和检索特定于子类型的数据。

- [处理专用部署](../../extensibility/internals/handling-specialized-deployment.md)

 说明项目子类型如何通过实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg>接口来提供专用部署行为。

- [添加和删除属性页](../../extensibility/adding-and-removing-property-pages.md)

 描述项目设计器中的添加和删除属性页。

## <a name="related-sections"></a>相关章节
- [项目类型](../../extensibility/internals/project-types.md)

 提供指向详细说明[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]项目的主题的链接。
