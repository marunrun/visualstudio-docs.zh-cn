---
title: 项目持久性 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- persistence, projects
- projects [Visual Studio SDK], persistance
ms.assetid: 42907bcf-4e27-46bd-a8cb-01c2ccd2bde5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 10a9cde91c0181fbfefbaa353c7c3702f4b36819
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706461"
---
# <a name="project-persistence"></a>项目持久性
持久性是项目的关键设计考虑因素。 大多数项目使用表示文件的项目项;[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]还支持数据非基于文件的项目。 必须保留项目拥有的文件和项目文件。 IDE 指示项目保存自身或项目项。

 项目的模板将传递到项目工厂。 模板应支持根据特定项目类型的要求对所有项目项进行初始化。 这些模板以后可以保存为项目文件，并由 IDE 通过解决方案进行管理。 有关详细信息，请参阅[使用项目工厂和解决方案创建项目实例](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)。 [Solutions](../../extensibility/internals/solutions-overview.md)

 项目项可以基于文件，也可以是非基于文件的：

- 基于文件的项可以是本地的，也可以是远程的。 例如，在 C# 中的 Web 项目中，与远程系统上文件的连接在本地保留，而文件本身则保留在远程系统上。

- 非基于文件的项可以将项保存到数据库或存储库。

## <a name="commit-models"></a>提交模型
 确定项目项的位置后，必须选择适当的提交模型。 例如，在具有本地文件的基于文件的模型中，可以自动保存每个项目。 在存储库模型中，可以在一个事务中保存多个项。 有关详细信息，请参阅[项目类型设计决策](../../extensibility/internals/project-type-design-decisions.md)。

 要确定文件名扩展名，项目实现<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>该接口，该接口提供的信息使对象的客户端能够实现 **"保存为"** 对话框，即填写 **"保存为类型"** 下拉列表并管理初始文件名扩展名。

 IDE 调用项目上`IPersistFileFormat`的接口以指示项目应保留其项目项。 因此，对象拥有其文件和格式的所有方面。 这包括对象的格式的名称。

 在项不是文件的情况下，`IPersistFileFormat`仍如何保留非基于文件的项。 还必须保留项目文件，如[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]项目的 .vbp 文件或[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]项目的 .vcproj 文件。

 对于保存操作，IDE 检查正在运行的文档表 （RDT），层次结构将命令传递给 和<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem><xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2>接口。 实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem.IsItemDirty%2A>该方法以确定项目是否已修改。 如果项有，<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem.SaveItem%2A>则实现该方法以保存修改后的项。

 接口上`IVsPersistHierarchyItem2`的方法用于确定是否可以重新加载项，如果可以重新加载项，则重新加载该项。 此外，还可以<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.IgnoreItemFileChanges%2A>实现该方法，以便在不保存的情况下丢弃已更改的项目。

## <a name="see-also"></a>请参阅
- [清单：新建项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)
- [使用项目工厂创建项目实例](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)
