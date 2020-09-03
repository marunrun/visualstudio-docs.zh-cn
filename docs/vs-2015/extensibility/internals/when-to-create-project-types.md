---
title: 何时创建项目类型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project types, conditions for creating
ms.assetid: 26adc860-ee4a-4f5c-95e1-e41b207dd7e6
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5b5bc2bacb53973bd552b983b742e4f9e68fe31b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65687697"
---
# <a name="when-to-create-project-types"></a>何时创建项目类型
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

创建新的项目类型提供了为用户自定义的基础 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。 但是，对于所有自定义项，不需要创建新的项目类型 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。 以下准则可帮助您确定方案是否需要新的项目类型。  
  
## <a name="create-a-new-project-type"></a>创建新的项目类型  
 如果要自定义 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 以下列一种或多种方式执行操作，则必须创建项目类型：  
  
- 参与生成、部署、配置和源代码管理。  
  
- 提供调试支持。  
  
- 在 **解决方案资源管理器**中显示项目项。  
  
- 使用 " **打开项目** " 或 " **新建项目** " 对话框。  
  
- 支持项目嵌套。  
  
## <a name="extend-an-existing-project-type"></a>扩展现有项目类型  
 你可能想要创建一个新的项目类型，该类型可使用 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 以下方法修改或扩展现有项目类型的行为，例如，修改项目的生成过程 [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] ：  
  
- 使用单个单元来处理多个文件。  
  
- 显示单个文件作为子项目的层次结构。  
  
- 在编辑器周围显示命令上下文。  
  
- 显示编辑器的服务上下文。  
  
## <a name="use-an-existing-project-type"></a>使用现有的项目类型  
 有时不需要创建新项目。 下表显示了不需要为其创建项目类型的任务。  
  
|任务|说明|  
|----------|-----------------|  
|处理命令|任何 VSPackage 都可以处理命令。|  
|生成编辑器|可以注册自定义编辑器。 有关详细信息，请参阅 [Document Windows And 编辑器](https://msdn.microsoft.com/603625e1-62b6-413a-bc44-089346e166bc)。|  
|拥有 windows|您可以创建工具窗口和文档窗口，而无需添加新的项目类型。|  
|公开属性窗口中的属性|所有对象都可以公开属性。|  
  
## <a name="create-a-project-subtype"></a>创建项目子类型  
 您可以使用项目子类型扩展托管项目类型，而不必创建新的项目类型。 项目子类型使用 COM 聚合来扩展以 Microsoft 或编写的托管项目 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] [!INCLUDE[csprcs](../../includes/csprcs-md.md)] 。 使用 COM 聚合，你可以重复使用多个托管项目系统实现，并且仍可通过聚合和使用支持接口自定义特定方案。 有关项目子类型的详细信息，请参阅 [项目子类型](../../extensibility/internals/project-subtypes.md)。  
  
## <a name="see-also"></a>另请参阅  
 [文档窗口和编辑器](https://msdn.microsoft.com/603625e1-62b6-413a-bc44-089346e166bc)   
 [清单：创建新的项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)   
 [Visual Studio 中的层次结构](../../extensibility/internals/hierarchies-in-visual-studio.md)
