---
title: 项目持久性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- persistence, projects
- projects [Visual Studio SDK], persistance
ms.assetid: 42907bcf-4e27-46bd-a8cb-01c2ccd2bde5
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: abbcc1fc1048866ef790a4b6779ed15ef80a9be1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62429517"
---
# <a name="project-persistence"></a>项目持久性
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

持久性是项目的重要设计注意事项。 大多数项目使用代表文件的项目项; [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 还支持其数据不是基于文件的项目。 项目和项目文件所拥有的文件必须保存。 IDE 指示项目保存自身或项目项。  
  
 项目模板会传递到项目工厂。 模板应支持根据特定项目类型的要求初始化所有项目项。 这些模板以后可以保存为项目文件，并由 IDE 通过解决方案进行管理。 有关详细信息，请参阅[使用项目工厂和解决方案创建项目实例](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)。 [Solutions](../../extensibility/internals/solutions-overview.md)  
  
 项目项可以是基于文件的，也可以是不基于文件的：  
  
- 基于文件的项可以是本地的，也可以是远程的。 例如，在 c # 中的 Web 项目中，到远程系统上的文件的连接将保留在本地，而文件本身将保留在远程系统上。  
  
- 非基于文件的项可以将项保存到数据库或存储库中。  
  
## <a name="commit-models"></a>提交模型  
 确定项目项的位置后，您必须选择适当的提交模型。 例如，在包含本地文件的基于文件的模型中，可以自主保存每个项目。 在存储库模型中，可以在一个事务中保存多个项。 有关详细信息，请参阅 [项目类型设计决策](../../extensibility/internals/project-type-design-decisions.md)。  
  
 为了确定文件扩展名，项目实现了 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat> 接口，该接口提供使对象的客户端实现 " **另存** 为" 对话框（即，在 " **保存类型** " 下拉列表中填写并管理初始文件扩展名）的信息。  
  
 IDE 将对 `IPersistFileFormat` 项目调用接口，以指示项目应适当地保留其项目项。 因此，对象拥有其文件和格式的所有方面。 这包括对象格式的名称。  
  
 如果项不是文件， `IPersistFileFormat` 则仍将保留非基于文件的项的持久性方式。 项目文件（如项目的 .vbp 文件 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 或项目的 vcproj 文件） [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] 也必须持久保存。  
  
 对于保存操作，IDE 将检查正在运行的文档表 (RDT) ，层次结构会将命令传递给 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2> 接口。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem.IsItemDirty%2A>实现方法以确定项是否已被修改。 如果项具有，则 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem.SaveItem%2A> 实现该方法以保存修改后的项。  
  
 接口上的方法 `IVsPersistHierarchyItem2` 用于确定是否可以重新加载项，如果项可以重新加载，则为。 此外，还 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.IgnoreItemFileChanges%2A> 可以实现此方法，以在不保存的情况下放弃更改的项。  
  
## <a name="see-also"></a>另请参阅  
 [清单：创建新的项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)   
 [使用项目工厂创建项目实例](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)
