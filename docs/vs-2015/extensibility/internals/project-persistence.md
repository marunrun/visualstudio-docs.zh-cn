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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62429517"
---
# <a name="project-persistence"></a>项目持久性
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

持久性是你的项目的关键设计注意事项。 大多数项目使用项目项代表文件;[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]还支持其数据是不基于文件的项目。 必须保留这两个拥有的项目和项目文件的文件。 IDE 指示要保存本身或项目项的项目。  
  
 项目的模板将传递给项目工厂。 模板应支持根据特定项目类型的要求的所有项目项的初始化。 这些模板稍后可以另存为项目文件，由该解决方案通过 IDE 管理。 有关详细信息，请参阅[创建项目实例通过使用项目工厂](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)并[解决方案](../../extensibility/internals/solutions-overview.md)。  
  
 项目项可以是基于文件的或非基于文件的：  
  
- 基于文件的项可以是本地或远程。 在 C# 中的 Web 项目，例如，将连接到远程系统上的文件保留本地，而在远程系统上保留文件本身。  
  
- 不基于文件的项可以将项目保存到数据库或存储库。  
  
## <a name="commit-models"></a>提交模型  
 在决定后的项目项的位置，必须选择相应提交模型。 例如，在基于文件的模型中使用本地文件，每个项目可以保存自主操作。 在存储库模型中，您可以保存在一个事务中的多个项。 有关详细信息，请参阅[项目类型设计决策](../../extensibility/internals/project-type-design-decisions.md)。  
  
 若要确定文件扩展名，项目实现<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>接口，它提供了信息使客户端对象的实现**另存为**对话框的 — 即，填写**保存类型**下拉列表列出和管理的初始文件扩展名。  
  
 IDE 调用`IPersistFileFormat`接口以指示该项目应保持其项目的项目项根据需要。 因此，该对象拥有其文件和格式的所有方面。 这包括对象的格式的名称。  
  
 项不是文件，以防`IPersistFileFormat`仍是如何非基于文件的项会被保留。 项目文件，如.vbp 文件[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]项目或.vcproj 文件[!INCLUDE[vcprvc](../../includes/vcprvc-md.md)]项目，也必须持久保存。  
  
 对于保存操作，IDE 会检查正在运行的 document 表 (RDT) 和层次结构将命令传递给<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2>接口。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem.IsItemDirty%2A>实现方法是为了确定是否已修改此项。 如果该项，<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem.SaveItem%2A>实现方法是为了保存已修改的项。  
  
 上的方法`IVsPersistHierarchyItem2`接口用于确定是否可以重新加载项，如果可以将项，重新加载它。 此外，<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.IgnoreItemFileChanges%2A>方法可以实现导致要放弃未保存的已更改的项。  
  
## <a name="see-also"></a>请参阅  
 [清单：创建新的项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)   
 [使用项目工厂创建项目实例](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)
