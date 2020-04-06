---
title: 项目类型要点 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types [Visual Studio SDK]
ms.assetid: 09991589-2300-430e-b6a4-7f2b95fe676f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b44da532207668d9526aec0ccdcab027b94184e6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706383"
---
# <a name="project-type-essentials"></a>项目类型基础知识
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]包括语言（如 或[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)][!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]） 的多个项目类型。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]还允许您创建自己的项目类型。

 如果只想向 添加自定义命令、编辑器或工具窗口[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]，则可以在不创建新项目类型的情况下执行此操作。 有关详情，请参阅以下主题：

- [命令、菜单和工具栏](../../extensibility/internals/commands-menus-and-toolbars.md)

- [编辑器和语言服务扩展](../../extensibility/editor-and-language-service-extensions.md)

- [扩展和自定义工具窗口](../../extensibility/extending-and-customizing-tool-windows.md)

  同样，如果要自定义提供的[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]和[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]项目类型的行为，则可以使用项目子类型执行此操作。 有关详细信息，请参阅[项目子类型](../../extensibility/internals/project-subtypes.md)。

  您必须为基于以下语言以外的[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]语言的项目创建新的项目类型，[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]如果要支持以下一种或多项：

- 生成

- 部署

- 多种配置

- 源代码管理

- 调试

- 解决方案资源管理器中的项目项

- **"打开项目**"或 **"新项目"** 对话框

- 项目嵌套

- 有关项目类型功能的详细信息，请参阅以下内容：

- 项目类型是 VSPackage 中实现预期接口[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]集的对象。 如果使用 C# 开发项目类型，托管包框架项目类将实现必要的接口，并允许您继承该实现。 有关详细信息，请参阅[使用托管包框架实现项目类型 （C#）。](../../extensibility/internals/using-the-managed-package-framework-to-implement-a-project-type-csharp.md)

- 对于C++开发人员来说，HierUtil 库中的类的工作方式类似。 有关详细信息，请参阅[不在生成中：使用 HierUtil7 项目类实现项目类型 （C++）。](https://msdn.microsoft.com/library/a5c16a09-94a2-46ef-87b5-35b815e2f346)

- 项目类型可以支持生成到 .exe 或 .dll 程序集的典型源代码文件以外的数据。 例如，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]数据库项目包含对存储在磁盘上的脚本和查询文件的引用，并将命令添加到**解决方案资源管理器**以针对数据库执行脚本和查询，但项目不支持生成行为。 有关详细信息，请参阅[打开和保存项目项目](../../extensibility/internals/opening-and-saving-project-items.md)。

- 项目类型根本不需要使用文件。 例如，项目类型可以将其所有数据存储在数据库中。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]使项目类型完全控制它们如何持久化项目和项目项的数据。 有关详细信息，请参阅[项目类型设计决策](../../extensibility/internals/project-type-design-decisions.md)。

- 项目类型必须提供*项目工厂*，这是一个对象，每当被告知打开或创建基于该项目类型的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]项目时，该对象都会创建项目类型的实例。 有关详细信息，请参阅[使用项目工厂创建项目实例](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)。

- 项目类型必须为项目和项目项提供模板。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]当用户创建新项目并将新项目添加到现有项目时，使用模板。 有关详细信息，请参阅[添加项目和项目项目模板](../../extensibility/internals/adding-project-and-project-item-templates.md)。

- 项目类型可以支持多种配置，如调试和发布。 用户可以使用您提供的属性页更改项目的不同配置。 有关详细信息，请参阅[管理配置选项](../../extensibility/internals/managing-configuration-options.md)。

## <a name="see-also"></a>请参阅
- [部署项目类型](../../extensibility/internals/deploying-project-types.md)
