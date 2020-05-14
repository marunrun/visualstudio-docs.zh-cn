---
title: 项目类型 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types, adding
- projects [Visual Studio SDK], adding new types
ms.assetid: 263a084f-f97a-4e09-add7-f0e8a6a27daf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6b343eeeee0912a6e9cad57ca6d35c33845e4dd4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706264"
---
# <a name="project-types"></a>项目类型
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]包括语言（如 和[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)][!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]） 的多个项目类型。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]还允许您创建自己的项目类型。

## <a name="in-this-section"></a>本节内容
- [概要](../../extensibility/internals/project-type-essentials.md)

 显示必须开始处理项目类型的重要信息。

- [创建项目类型](../../extensibility/internals/creating-project-types.md)

 讨论项目类型的设计。

- [将命令添加到解决方案资源管理器工具栏](../../extensibility/adding-a-command-to-the-solution-explorer-toolbar.md)

 详细说明向[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]**解决方案资源管理器**工具栏添加按钮必须遵循的步骤。

- [添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)

 讨论如何向项目类型添加模板，以便用户可以根据模式创建新项目和项目项。

- [打开和保存项目项](../../extensibility/internals/opening-and-saving-project-items.md)

 提供有关如何管理项目类型支持的项的信息。

- [管理配置选项](../../extensibility/internals/managing-configuration-options.md)

 讨论项目类型如何支持配置选项，如调试和发布，这些选项控制项目的生成、调试方式等。

- [支持源代码管理](../../extensibility/internals/supporting-source-control.md)

 提供有关如何向项目类型添加对源代码管理系统的支持的信息。

- [嵌套项目](../../extensibility/internals/nesting-projects.md)

 说明项目类型如何支持*嵌套*，以便可以在**解决方案资源管理器**中将项目分组在一起。

- [升级项目](../../extensibility/internals/upgrading-projects.md)

 描述项目类型如何参与升级向导，以从[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]的早期版本升级项目文件。

- [体系结构](../../extensibility/internals/project-types-architecture.md)

 提供有关项目类型的详细技术信息。

## <a name="related-sections"></a>相关章节
- [层次结构和选择](../../extensibility/internals/hierarchies-and-selection.md)

 概述了[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]集成开发环境 （IDE） 如何将项目显示为层次结构。

- [项目子类型](../../extensibility/internals/project-subtypes.md)

 提供指向项目子类型主题的链接。 项目子类型支持大多数项目类型的扩展，包括您自己的项目类型。

- [项目](../../extensibility/internals/projects.md)

 描述如何扩展[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]项目系统。
