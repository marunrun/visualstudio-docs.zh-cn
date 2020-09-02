---
title: 项目模型的元素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], implementation considerations
- project models
- projects [Visual Studio SDK], elements
ms.assetid: a1dbe0dc-68da-45d7-8704-5b43ff7e4fc4
caps.latest.revision: 19
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0f3b07068939e34b5c9e9487761177c0e12f5654
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65700125"
---
# <a name="elements-of-a-project-model"></a>项目模型的元素
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

中所有项目的接口和实现 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 共享基本结构：项目类型的项目模型。 在你要开发的 VSPackage 中，你可以创建符合设计决策的对象，并与 IDE 提供的全局功能一起工作。 例如，你可以控制如何保存项目项，但你不会控制必须保存文件的通知。 当用户将焦点放在打开的项目项上并在菜单栏上的 "**文件**" 菜单中选择 "**保存**" 时 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ，项目类型代码必须截获 ide 中的命令，保存该文件，然后将通知发送回 ide，指出该文件不再发生更改。  
  
 你的 VSPackage 通过提供对 IDE 接口的访问的服务与 IDE 交互。 例如，通过特定服务，可以监视和路由命令，并提供在项目中所做选择的上下文信息。 VSPackage 所需的所有全局 IDE 功能都是由服务提供的。 有关服务的详细信息，请参阅 [如何：获取服务](../../extensibility/how-to-get-a-service.md)。  
  
 其他实现注意事项：  
  
- 单个项目模型可以包含多个项目类型。  
  
- 项目类型和助理项目工厂单独注册为 Guid。  
  
- 当用户通过 UI 创建新项目时，每个项目都必须有一个模板文件或向导来初始化新的项目文件 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。 例如， [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] 模板会初始化最终成为 vcproj 文件的内容。  
  
  下图显示了组成典型项目实现的主接口、服务和对象。 您可以使用应用程序帮助程序 HierUtil7 来创建基础对象和其他编程样板。 有关 HierUtil7 应用程序帮助器的详细信息，请参阅 [不在生成中：使用 HierUtil7 项目类实现项目类型 (c + +) ](https://msdn.microsoft.com/a5c16a09-94a2-46ef-87b5-35b815e2f346)。  
  
  ![Visual Studio 项目模型图](../../extensibility/internals/media/vsprojectmodel.gif "vsProjectModel")  
  项目模型  
  
  若要详细了解上图中列出的接口和服务，以及关系图中未包含的其他可选接口，请参阅 [项目模型核心组件](../../extensibility/internals/project-model-core-components.md)。  
  
  项目可以支持命令，因此必须实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 接口以通过命令上下文 guid 参与命令路由。  
  
## <a name="see-also"></a>另请参阅  
 [清单：创建新的项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)   
 [不在生成中：使用 HierUtil7 项目类实现项目类型 (c + +) ](https://msdn.microsoft.com/a5c16a09-94a2-46ef-87b5-35b815e2f346)   
 [项目模型核心组件](../../extensibility/internals/project-model-core-components.md)   
 [使用项目工厂创建项目实例](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)   
 [如何：获取服务](../../extensibility/how-to-get-a-service.md)   
 [创建项目类型](../../extensibility/internals/creating-project-types.md)
