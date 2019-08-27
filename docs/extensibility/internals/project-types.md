---
title: 项目类型 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types, adding
- projects [Visual Studio SDK], adding new types
ms.assetid: 263a084f-f97a-4e09-add7-f0e8a6a27daf
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a8d41eb5b21dc22ca0345c9cbf93ce680354d0db
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66318765"
---
# <a name="project-types"></a>项目类型
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 包括几种语言的项目类型，如[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]和[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 此外可以创建自己的项目类型。

## <a name="in-this-section"></a>本节内容
- [基础知识](../../extensibility/internals/project-type-essentials.md)

 显示必须具有以开始使用的项目类型的重要信息。

- [创建项目类型](../../extensibility/internals/creating-project-types.md)

 讨论有关项目类型的设计。

- [将命令添加到解决方案资源管理器工具栏](../../extensibility/adding-a-command-to-the-solution-explorer-toolbar.md)

 详细介绍添加到按钮时必须遵循的步骤[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]**解决方案资源管理器**工具栏。

- [添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)

 讨论如何为您的项目类型添加模板，以便用户可以创建新项目和项目项根据一种模式。

- [打开和保存项目项](../../extensibility/internals/opening-and-saving-project-items.md)

 提供有关如何管理您的项目类型支持的项的信息。

- [管理配置选项](../../extensibility/internals/managing-configuration-options.md)

 讨论如何项目类型可支持配置选项，如调试和发布，用于控制如何生成项目，调试，等等。

- [支持源代码管理](../../extensibility/internals/supporting-source-control.md)

 提供有关如何将源代码管理系统的支持添加到您项目的类型信息。

- [嵌套项目](../../extensibility/internals/nesting-projects.md)

 介绍如何支持项目类型*嵌套*，以便项目可以集中归入**解决方案资源管理器**。

- [升级项目](../../extensibility/internals/upgrading-projects.md)

 介绍如何在项目类型可以参与升级向导来升级项目文件从早期版本的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。

- [体系结构](../../extensibility/internals/project-types-architecture.md)

 提供有关项目类型的详细技术信息。

## <a name="related-sections"></a>相关章节
- [层次结构和选择](../../extensibility/internals/hierarchies-and-selection.md)

 概述了如何[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]集成的开发环境 (IDE) 显示为层次结构的一个项目。

- [项目子类型](../../extensibility/internals/project-subtypes.md)

 提供指向项目子类型的主题的链接。 项目子类型启用的大多数类型的项目类型，包括你自己的扩展。

- [项目](../../extensibility/internals/projects.md)

 介绍如何扩展[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]项目系统。