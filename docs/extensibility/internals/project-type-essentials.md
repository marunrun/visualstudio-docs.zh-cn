---
title: 项目类型基础 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types [Visual Studio SDK]
ms.assetid: 09991589-2300-430e-b6a4-7f2b95fe676f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 435d3ca0e35911754cac1e37abb276939109a0b3
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72725411"
---
# <a name="project-type-essentials"></a>项目类型基础知识
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 包括 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 或 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 等语言的多种项目类型。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 还允许您创建自己的项目类型。

 如果只是想要将自定义命令、编辑器或工具窗口添加到 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]，则无需创建新的项目类型即可执行此操作。 有关更多信息，请参见下列主题：

- [命令、菜单和工具栏](../../extensibility/internals/commands-menus-and-toolbars.md)

- [编辑器和语言服务扩展](../../extensibility/editor-and-language-service-extensions.md)

- [扩展和自定义工具窗口](../../extensibility/extending-and-customizing-tool-windows.md)

  同样，如果要自定义所提供的 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 和 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 项目类型的行为，则可以使用项目子类型执行此操作。 有关详细信息，请参阅[项目子类型](../../extensibility/internals/project-subtypes.md)。

  如果要支持以下一种或多种语言，则必须为基于非 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 语言的项目创建新的项目类型：

- 生成

- 部署

- 多个配置

- 源代码管理

- 调试

- 解决方案资源管理器中的项目项

- "**打开项目**" 或 "**新建项目**" 对话框

- 项目嵌套

- 有关项目类型的功能的详细信息，请参阅以下内容：

- 项目类型是 VSPackage 中实现所需 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 接口集的对象。 如果使用C#来开发项目类型，托管包框架项目类将为你实现所需的接口，并允许你继承该实现。 有关详细信息，请参阅[使用托管包框架实现项目类型（C#）](../../extensibility/internals/using-the-managed-package-framework-to-implement-a-project-type-csharp.md)。

- 对于C++开发人员而言，HierUtil 库中的类的工作方式类似。 有关详细信息，请参阅[不在生成中：使用 HierUtil7 项目类实现项目类型（C++）](https://msdn.microsoft.com/library/a5c16a09-94a2-46ef-87b5-35b815e2f346)。

- 项目类型可以支持生成到 .exe 或 .dll 程序集中的典型源代码文件以外的其他数据。 例如，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 数据库项目包含对磁盘上存储的脚本和查询文件的引用，并向**解决方案资源管理器**添加命令以对数据库执行脚本和查询，但这些项目不支持生成行为。 有关详细信息，请参阅[打开和保存项目项](../../extensibility/internals/opening-and-saving-project-items.md)。

- 项目类型根本不必使用文件。 例如，项目类型可以将其所有数据存储在数据库中。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 可以使项目类型完全控制其如何保存项目和项目项的数据。 有关详细信息，请参阅[项目类型设计决策](../../extensibility/internals/project-type-design-decisions.md)。

- 项目类型必须提供一个*项目工厂*，它是一个对象，该对象在每次告知 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 时创建项目类型的实例，或创建一个基于该项目类型的项目。 有关详细信息，请参阅[使用项目工厂创建项目实例](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)。

- 项目类型必须提供项目和项目项的模板。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 在用户创建新项目并向现有项目中添加新项时使用模板。 有关详细信息，请参阅[添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)。

- 项目类型可以支持多个配置，例如调试和发布。 用户可以使用所提供的属性页更改项目的不同配置。 有关详细信息，请参阅[管理配置选项](../../extensibility/internals/managing-configuration-options.md)。

## <a name="see-also"></a>请参阅
- [部署项目类型](../../extensibility/internals/deploying-project-types.md)