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
ms.openlocfilehash: 8be01ef0592deab48d923828ccfd3f86f1311a4d
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66323061"
---
# <a name="when-to-create-project-types"></a>何时创建项目类型
为自定义创建新的项目类型提供了基础[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]为你的用户。 但是，创建新的项目类型不是必需的所有[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]自定义项。 以下指导原则应帮助您确定是否需要为你的方案的新项目类型。

## <a name="create-a-new-project-type"></a>创建新的项目类型
 如果想要自定义，则必须创建一种项目类型[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]以充当一个或多个通过以下方式：

- 参与生成、 部署、 配置和源代码管理。

- 调试支持的产品/服务。

- 显示中的项目项**解决方案资源管理器**。

- 使用**打开项目**或**新项目**对话框。

- 支持项目嵌套。

## <a name="extend-an-existing-project-type"></a>扩展现有项目类型
 你可能想要创建新的项目类型，可以使用[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]按以下方式来修改或扩展现有项目类型的行为，例如，修改的生成过程[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]项目：

- 处理多个文件作为单个单元。

- 显示为子项目的层次结构的单个文件。

- 显示有关编辑器命令上下文。

- 显示服务上下文的编辑器。

## <a name="use-an-existing-project-type"></a>使用现有的项目类型
 创建新的项目有时不是必需。 下表显示了不需要创建的项目类型的任务。

|任务|描述|
|----------|-----------------|
|处理命令|任何 VSPackage 可以处理命令。|
|生成编辑器|可以注册自定义编辑器。 有关详细信息，请参阅[文档 Windows 和编辑器](https://msdn.microsoft.com/library/603625e1-62b6-413a-bc44-089346e166bc)。|
|拥有 windows|可以创建工具和文档窗口，而不添加新的项目类型。|
|在属性窗口中公开属性|所有对象可以都公开属性。|

## <a name="create-a-project-subtype"></a>创建项目子类型
 项目子类型可用于扩展托管的项目类型，而无需创建新的项目类型。 项目子类型使用 COM 聚合来扩展托管的项目中编写的 Microsoft[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]或[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]。 使用 COM 聚合，可以重复使用的托管的项目系统实现大部分并仍然通过聚合和使用支持接口为特定方案自定义。 有关项目子类型的详细信息，请参阅[项目子类型](../../extensibility/internals/project-subtypes.md)。

## <a name="see-also"></a>请参阅
- [文档 Windows 和编辑器](https://msdn.microsoft.com/library/603625e1-62b6-413a-bc44-089346e166bc)
- [清单：创建新的项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)
- [Visual Studio 中的层次结构](../../extensibility/internals/hierarchies-in-visual-studio.md)