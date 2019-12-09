---
title: 用于输出的项目配置 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project configurations, output
ms.assetid: a4517f73-45af-4745-9d7f-9fddf887b636
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: addd7e8630ce35c6bdbbbb4c063197f75a74c97d
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74300678"
---
# <a name="project-configuration-for-output"></a>用于输出的项目配置
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

每个配置都可以支持生成可执行文件或资源文件等输出项的一组生成过程。 这些输出项专用于用户，并且可放置在链接相关类型的输出（如可执行文件（.exe、.dll、.lib）和源文件（.idl、.h 文件）的组中。  
  
 可以通过 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutput2> 方法提供输出项，并使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumOutputs> 方法进行枚举。 如果要对输出项进行分组，则项目还应实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputGroup> 接口。  
  
 通过实现 `IVsOutputGroup` 开发的构造允许项目根据使用情况对输出进行分组。 例如，DLL 可能与程序数据库（PDB）组合在一起。  
  
> [!NOTE]
> PDB 文件包含调试信息，并且在生成 .dll 或 .exe 时指定了 "生成调试信息" 选项时创建。 通常只为调试项目配置生成 .pdb 文件。  
  
 项目必须为其支持的每个配置返回相同数量的组，即使组中包含的输出数可能因配置而异。 例如，project Matt 的 DLL 可能在调试配置中包含 mattd 和 mattd，但在零售配置中只包含 Matt。  
  
 这些组的标识符信息（如规范名称、显示名称和组信息）在项目中的配置和配置中也有相同的标识符信息。 即使配置发生更改，也可以通过此一致性进行部署和打包操作。  
  
 组还可以有一个密钥输出，它允许打包快捷方式指向一些有意义的内容。 在给定的配置中，任何组都可能为空，因此不应对组的大小进行任何假设。 任何配置中的每个组的大小（输出数）可以不同于同一配置中其他组的大小。 它还可以与另一配置中相同组的大小不同。  
  
 ![输出组图](../../extensibility/internals/media/vsoutputgroups.gif "vsOutputGroups")  
输出组  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg> 接口的主要用途是提供对生成、部署和调试管理对象的访问，并允许项目自由地对输出进行分组。 有关使用此接口的详细信息，请参阅[项目配置对象](../../extensibility/internals/project-configuration-object.md)。  
  
 在前面的关系图中，"生成组" 在配置（"bD" 或 ".exe"）上有一个密钥输出，因此，用户可以创建一个快捷方式来构建，知道无论部署的配置如何，快捷方式都可以正常工作。 组源没有密钥输出，因此用户无法创建它的快捷方式。 如果生成的调试组具有密钥输出，但生成的零售组不是，则不是正确实现。 接下来，如果有任何配置具有不包含任何输出的组，并且由于没有密钥文件，则具有包含输出的该组的其他配置不能包含密钥文件。 安装程序编辑器假定组的规范名称和显示名称以及密钥文件的存在，不会根据配置进行更改。  
  
 请注意，如果项目有不想打包或部署的 `IVsOutputGroup`，则必须将该输出放入组中。 仍可通过实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg.EnumOutputs%2A> 方法来正常枚举输出，该方法将返回配置的所有输出，而不考虑分组。  
  
 有关详细信息，请参阅[用于项目的 MPF](https://archive.codeplex.com/?p=mpfproj12)上的自定义项目示例中的 `IVsOutputGroup` 实现。  
  
## <a name="see-also"></a>请参阅  
 [管理配置选项](../../extensibility/internals/managing-configuration-options.md)   
 [用于生成  的项目配置](../../extensibility/internals/project-configuration-for-building.md)  
 [项目配置对象](../../extensibility/internals/project-configuration-object.md)   
 [解决方案配置](../../extensibility/internals/solution-configuration.md)
