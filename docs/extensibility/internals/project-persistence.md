---
title: 项目持久性 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- persistence, projects
- projects [Visual Studio SDK], persistance
ms.assetid: 42907bcf-4e27-46bd-a8cb-01c2ccd2bde5
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a95c919de9b87ed1782cbdcb029efbf191958f5a
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72725453"
---
# <a name="project-persistence"></a>项目持久性
持久性是项目的重要设计注意事项。 大多数项目使用代表文件的项目项;[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 还支持其数据不是基于文件的项目。 项目和项目文件所拥有的文件必须保存。 IDE 指示项目保存自身或项目项。

 项目模板会传递到项目工厂。 模板应支持根据特定项目类型的要求初始化所有项目项。 这些模板以后可以保存为项目文件，并由 IDE 通过解决方案进行管理。 有关详细信息，请参阅[使用项目工厂](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)和[解决方案](../../extensibility/internals/solutions-overview.md)创建项目实例。

 项目项可以是基于文件的，也可以是不基于文件的：

- 基于文件的项可以是本地的，也可以是远程的。 例如，在中C#的 Web 项目中，到远程系统上的文件的连接将保留在本地，而文件本身将保留在远程系统上。

- 非基于文件的项可以将项保存到数据库或存储库中。

## <a name="commit-models"></a>提交模型
 确定项目项的位置后，您必须选择适当的提交模型。 例如，在包含本地文件的基于文件的模型中，可以自主保存每个项目。 在存储库模型中，可以在一个事务中保存多个项。 有关详细信息，请参阅[项目类型设计决策](../../extensibility/internals/project-type-design-decisions.md)。

 为了确定文件扩展名，项目实现 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat> 接口，该接口提供使对象的客户端实现 "**另存**为" 对话框的信息，即填写 "**保存类型**" 下拉列表并管理初始文件扩展名。

 IDE 将对项目调用 `IPersistFileFormat` 接口，以指示项目应适当地保留其项目项。 因此，对象拥有其文件和格式的所有方面。 这包括对象格式的名称。

 如果项目不是文件，则 `IPersistFileFormat` 仍是指非基于文件的项目是如何持久的。 项目文件（如 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 项目的 .vbp 文件或 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 项目的 vcproj 文件）也必须持久保存。

 对于保存操作，IDE 将检查正在运行的文档表（RDT），层次结构会将命令传递到 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2> 接口。 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem.IsItemDirty%2A> 方法，以确定该项是否已被修改。 如果项具有，则实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem.SaveItem%2A> 方法来保存修改后的项。

 `IVsPersistHierarchyItem2` 接口上的方法用于确定是否可以重新加载项，如果项可以重新加载，则为。 此外，还可以实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.IgnoreItemFileChanges%2A> 方法，以便在不保存的情况下放弃更改的项。

## <a name="see-also"></a>请参阅
- [清单：创建新的项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)
- [使用项目工厂创建项目实例](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)