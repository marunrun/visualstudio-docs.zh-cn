---
title: 项目子类型 |Microsoft Docs
description: 了解项目子类型如何允许自定义 Visual Studio 的项目系统的行为。 Vspackage 使用 COM 聚合来实现项目子类型。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 05240ee72aef85e50d07c7a39df1c819f04933a2
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2021
ms.locfileid: "97876293"
---
# <a name="project-subtypes"></a>项目子类型
项目子类型使你可以自定义或风格的项目系统的行为 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 自定义包括将其他数据保存在项目文件中、在 " **添加新项** " 对话框中添加或筛选项、控制程序集的调试和部署方式以及扩展 "项目 **属性页** " 对话框。 Vspackage 使用 COM 聚合来实现项目子类型。

> [!NOTE]
> Visual C++ 项目系统不支持项目子类型。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 本身使用项目子类型来实现 SQL Server 和智能设备项目。

## <a name="in-this-section"></a>本节内容

- [项目子类型设计](../../extensibility/internals/project-subtypes-design.md)

  介绍项目子类型的概念。

- [项目子类型的初始化序列](../../extensibility/internals/initialization-sequence-of-project-subtypes.md)

  按环境描述编程项目子类型初始化顺序 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

- [项目子类型扩展的属性和方法](../../extensibility/internals/properties-and-methods-extended-by-project-subtypes.md)

  提供使用项目子类型最常扩展的功能和方法的详细说明。

- [保留 MSBuild 项目文件中的数据](../../extensibility/internals/persisting-data-in-the-msbuild-project-file.md)

  介绍如何在项目文件中持久保存数据，以及如何使用 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> 跨项目子类型聚合级别维护项目文件中的数据。

- [项目属性用户界面](../../extensibility/internals/project-property-user-interface.md)

  介绍项目子类型如何修改 "项目 **属性页** " 对话框。

- [扩展基项目的对象模型](../../extensibility/internals/extending-the-object-model-of-the-base-project.md)

  提供有关项目子类型如何使用自动化扩展程序来扩展自动化对象模型的信息。

- [构成“添加新项”对话框](../../extensibility/internals/contributing-to-the-add-new-item-dialog-box.md)

  描述如何将项添加到 " **添加新项** " 对话框。

- [将数据保存在项目文件中](../../extensibility/saving-data-in-project-files.md)

  说明项目子类型如何使用托管包框架 (MPF) 来保存和检索项目文件中特定于子类型的数据。

- [处理专用部署](../../extensibility/internals/handling-specialized-deployment.md)

  说明项目子类型如何通过实现接口来提供专用的部署行为 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg> 。

- [添加和删除属性页](../../extensibility/adding-and-removing-property-pages.md)

  介绍如何在 "项目设计器" 中添加和删除属性页。

## <a name="related-sections"></a>相关章节

- [项目类型](../../extensibility/internals/project-types.md)

  提供一些主题链接，这些主题详细介绍了 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 项目。
