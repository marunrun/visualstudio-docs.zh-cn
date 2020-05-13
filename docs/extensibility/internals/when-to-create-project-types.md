---
title: 何时创建项目类型 |微软文档
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
ms.openlocfilehash: 861250dac25288f353cbd5c57f510bf67dadce70
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703435"
---
# <a name="when-to-create-project-types"></a>何时创建项目类型
创建新项目类型为用户自定义[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]提供了基础。 但是，并非所有自定义项都需要[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]创建新的项目类型。 以下指南将帮助您确定方案是否需要新的项目类型。

## <a name="create-a-new-project-type"></a>创建新项目类型
 如果要自定义[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]以以下一种或多种方式操作，则必须创建项目类型：

- 参与生成、部署、配置和源代码管理。

- 提供调试支持。

- 在**解决方案资源管理器**中显示项目项。

- 使用 **"打开项目**"或 **"新项目"** 对话框。

- 支持项目嵌套。

## <a name="extend-an-existing-project-type"></a>扩展现有项目类型
 您可能希望创建新的项目类型，该类型可通过以下方式修改[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]或扩展现有项目类型的行为，例如，修改[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]项目的生成过程：

- 将多个文件用作单个单元。

- 将单个文件显示为子项的层次结构。

- 在编辑器周围显示命令上下文。

- 显示编辑器的服务上下文。

## <a name="use-an-existing-project-type"></a>使用现有项目类型
 有时不需要创建新项目。 下表显示了不必为其创建项目类型的任务。

|任务|描述|
|----------|-----------------|
|处理命令|任何 VS 包都可以处理命令。|
|构建编辑器|可以注册自定义编辑器。 有关详细信息，请参阅[文档窗口和编辑器](https://msdn.microsoft.com/library/603625e1-62b6-413a-bc44-089346e166bc)。|
|拥有窗口|您可以创建工具和文档窗口，而无需添加新的项目类型。|
|在"属性"窗口中公开属性|所有对象都可以公开属性。|

## <a name="create-a-project-subtype"></a>创建项目子类型
 可以使用项目子类型扩展托管项目类型，而无需创建新的项目类型。 项目子类型使用 COM 聚合来扩展在 Microsoft [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]或 中编写的托管项目。 使用 COM 聚合，您可以重用大部分托管项目系统实现，并且仍然通过聚合和使用支持接口对特定方案进行自定义。 有关项目子类型的详细信息，请参阅[项目子类型](../../extensibility/internals/project-subtypes.md)。

## <a name="see-also"></a>请参阅
- [文档窗口和编辑器](https://msdn.microsoft.com/library/603625e1-62b6-413a-bc44-089346e166bc)
- [清单：新建项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)
- [Visual Studio 中的层次结构](../../extensibility/internals/hierarchies-in-visual-studio.md)
