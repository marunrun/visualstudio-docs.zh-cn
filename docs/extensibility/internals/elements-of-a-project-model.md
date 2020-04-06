---
title: 项目模型的元素 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], implementation considerations
- project models
- projects [Visual Studio SDK], elements
ms.assetid: a1dbe0dc-68da-45d7-8704-5b43ff7e4fc4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cf847e35878dc84bb32fe81053c01c23e565fc4c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708526"
---
# <a name="elements-of-a-project-model"></a>项目模型的元素
中[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]所有项目的接口和实现共享一个基本结构：项目类型的项目模型。 在项目模型中（即您正在开发的 VSPackage）中，您将创建符合设计决策的对象，并与 IDE 提供的全局功能协同工作。 例如，尽管控制项目项的保留方式，但不控制必须保留文件的通知。 当用户将焦点放在打开的项目项上并选择 **"保存在**[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]**菜单栏上的文件**"菜单上时，项目类型代码必须拦截 IDE 的命令，保留文件，并将文件发送回 IDE，通知文件不再更改。

 您的 VS 包通过提供对 IDE 接口的访问的服务与 IDE 进行交互。 例如，通过特定服务，您可以监视和路由命令，并为项目中所做的选择提供上下文信息。 VSPackage 所需的所有全球 IDE 功能均由服务提供。 有关服务的详细信息，请参阅[如何：获取服务](../../extensibility/how-to-get-a-service.md)。

 其他实现注意事项：

- 单个项目模型可以包含多个项目类型。

- 项目类型和相应的项目工厂在 GUID 中独立注册。

- 当用户通过[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]UI 创建新项目时，每个项目都必须具有模板文件或向导来初始化新项目文件。 例如，[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]模板初始化最终成为 .vcproj 文件的内容。

  下图显示了构成典型项目实现的主要接口、服务和对象。 您可以使用应用程序帮助器`HierUtil7`，创建基础对象和其他编程样板。 有关`HierUtil7`应用程序帮助程序的详细信息，请参阅[使用 HierUtil7 项目类来实现项目类型 （C++）](https://msdn.microsoft.com/library/a5c16a09-94a2-46ef-87b5-35b815e2f346)。

  ![可视化工作室项目模型图形](../../extensibility/internals/media/vsprojectmodel.gif "vs 项目模型")项目模型

  有关上图中列出的接口和服务以及关系图中未包括的其他可选接口的详细信息，请参阅[Project 模型核心组件](../../extensibility/internals/project-model-core-components.md)。

  项目可以支持命令，因此必须实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口才能通过命令上下文 GUID 参与命令路由。

## <a name="see-also"></a>请参阅
- [检查表：创建新的项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)
- [使用 HierUtil7 项目类实现项目类型 （C++）](https://msdn.microsoft.com/library/a5c16a09-94a2-46ef-87b5-35b815e2f346)
- [项目模型核心组件](../../extensibility/internals/project-model-core-components.md)
- [使用项目工厂创建项目实例](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)
- [如何：获取服务](../../extensibility/how-to-get-a-service.md)
- [创建项目类型](../../extensibility/internals/creating-project-types.md)
