---
title: 何时创建项目类型 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types, conditions for creating
ms.assetid: 26adc860-ee4a-4f5c-95e1-e41b207dd7e6
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ff29843965c220c505266a9cd973e5695c0b9dab
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72721557"
---
# <a name="when-to-create-project-types"></a>何时创建项目类型
创建新的项目类型提供了为用户自定义 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 的基础。 但是，所有 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 自定义项都不需要创建新的项目类型。 以下准则可帮助您确定方案是否需要新的项目类型。

## <a name="create-a-new-project-type"></a>创建新的项目类型
 如果要使用以下一种或多种方式自定义要执行的 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]，则必须创建项目类型：

- 参与生成、部署、配置和源代码管理。

- 提供调试支持。

- 在**解决方案资源管理器**中显示项目项。

- 使用 "**打开项目**" 或 "**新建项目**" 对话框。

- 支持项目嵌套。

## <a name="extend-an-existing-project-type"></a>扩展现有项目类型
 你可能想要创建一个新的项目类型，该类型可使用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 按以下方式修改或扩展现有项目类型的行为，例如修改 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 项目的生成过程：

- 使用单个单元来处理多个文件。

- 显示单个文件作为子项目的层次结构。

- 在编辑器周围显示命令上下文。

- 显示编辑器的服务上下文。

## <a name="use-an-existing-project-type"></a>使用现有的项目类型
 有时不需要创建新项目。 下表显示了不需要为其创建项目类型的任务。

|任务|描述|
|----------|-----------------|
|处理命令|任何 VSPackage 都可以处理命令。|
|生成编辑器|可以注册自定义编辑器。 有关详细信息，请参阅[Document Windows And 编辑器](https://msdn.microsoft.com/library/603625e1-62b6-413a-bc44-089346e166bc)。|
|拥有 windows|您可以创建工具窗口和文档窗口，而无需添加新的项目类型。|
|公开属性窗口中的属性|所有对象都可以公开属性。|

## <a name="create-a-project-subtype"></a>创建项目子类型
 您可以使用项目子类型扩展托管项目类型，而不必创建新的项目类型。 项目子类型使用 COM 聚合来扩展以 Microsoft [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 或 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 编写的托管项目。 使用 COM 聚合，你可以重复使用多个托管项目系统实现，并且仍可通过聚合和使用支持接口自定义特定方案。 有关项目子类型的详细信息，请参阅[项目子类型](../../extensibility/internals/project-subtypes.md)。

## <a name="see-also"></a>请参阅
- [文档窗口和编辑器](https://msdn.microsoft.com/library/603625e1-62b6-413a-bc44-089346e166bc)
- [清单：新建项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)
- [Visual Studio 中的层次结构](../../extensibility/internals/hierarchies-in-visual-studio.md)