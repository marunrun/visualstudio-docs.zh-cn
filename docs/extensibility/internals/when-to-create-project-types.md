---
title: 何时创建项目类型 |Microsoft Docs
description: 了解如何确定是否需要新的项目类型来为用户自定义 Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types, conditions for creating
ms.assetid: 26adc860-ee4a-4f5c-95e1-e41b207dd7e6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 458ca77ebcd8017b9834a8925edec255ca04cc13
ms.sourcegitcommit: 19061b61759ce8e3b083a0e01a858e5435580b3e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2020
ms.locfileid: "97487824"
---
# <a name="when-to-create-project-types"></a>何时创建项目类型
创建新的项目类型提供了为用户自定义的基础 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 但是，对于所有自定义项，不需要创建新的项目类型 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 以下准则可帮助您确定方案是否需要新的项目类型。

## <a name="create-a-new-project-type"></a>创建新的项目类型
 如果要自定义 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 以下列一种或多种方式执行操作，则必须创建项目类型：

- 参与生成、部署、配置和源代码管理。

- 提供调试支持。

- 在 **解决方案资源管理器** 中显示项目项。

- 使用 " **打开项目** " 或 " **新建项目** " 对话框。

- 支持项目嵌套。

## <a name="extend-an-existing-project-type"></a>扩展现有项目类型
 你可能想要创建一个新的项目类型，该类型可使用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 以下方法修改或扩展现有项目类型的行为，例如，修改项目的生成过程 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] ：

- 使用单个单元来处理多个文件。

- 显示单个文件作为子项目的层次结构。

- 在编辑器周围显示命令上下文。

- 显示编辑器的服务上下文。

## <a name="use-an-existing-project-type"></a>使用现有的项目类型
 有时不需要创建新项目。 下表显示了不需要为其创建项目类型的任务。

|任务|说明|
|----------|-----------------|
|处理命令|任何 VSPackage 都可以处理命令。|
|生成编辑器|可以注册自定义编辑器。 有关详细信息，请参阅 [Document Windows And 编辑器](/previous-versions/bb165691(v=vs.100))。|
|拥有 windows|您可以创建工具窗口和文档窗口，而无需添加新的项目类型。|
|公开属性窗口中的属性|所有对象都可以公开属性。|

## <a name="create-a-project-subtype"></a>创建项目子类型
 您可以使用项目子类型扩展托管项目类型，而不必创建新的项目类型。 项目子类型使用 COM 聚合来扩展以 Microsoft 或编写的托管项目 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 。 使用 COM 聚合，你可以重复使用多个托管项目系统实现，并且仍可通过聚合和使用支持接口自定义特定方案。 有关项目子类型的详细信息，请参阅 [项目子类型](../../extensibility/internals/project-subtypes.md)。

## <a name="see-also"></a>请参阅
- [文档窗口和编辑器](/previous-versions/bb165691(v=vs.100))
- [清单：创建新的项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)
- [Visual Studio 中的层次结构](../../extensibility/internals/hierarchies-in-visual-studio.md)