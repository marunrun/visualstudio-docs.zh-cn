---
title: 输出项目配置 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project configurations, output
ms.assetid: a4517f73-45af-4745-9d7f-9fddf887b636
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 78b95457af4c5d806fdfcc20f49ac4e82df36488
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706673"
---
# <a name="project-configuration-for-output"></a>用于输出的项目配置
每个配置都可以支持一组生成进程，这些生成进程生成输出项（如可执行文件或资源文件）。 这些输出项是用户专用的，可以放置在链接相关输出类型的组中，如可执行文件（.exe、.dll、.lib）和源文件（.idl、.h 文件）。

 输出项可以通过这些方法提供，<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutput2>并随<xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumOutputs>这些方法枚举。 如果要对输出项进行分组，项目还应实现接口<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputGroup>。

 通过实现`IVsOutputGroup`开发的构造允许项目根据使用情况对输出进行分组。 例如，DLL 可能与其程序数据库 （PDB） 进行分组。

> [!NOTE]
> PDB 文件包含调试信息，并在生成 .dll 或 .exe 时指定"生成调试信息"选项时创建该文件。 .pdb 文件通常仅用于调试项目配置。

 项目必须为其支持的每个配置返回相同数量的组，即使组中包含的输出数可能因配置而异。 例如，项目 Matt 的 DLL 可能包括调试配置中的 mattd.dll 和 mattd.pdb，但在零售配置中仅包括 matt.dll。

 从项目中的配置到配置，这些组还具有相同的标识符信息，如规范名称、显示名称和组信息。 这种一致性允许部署和打包继续运行，即使配置发生变化也是如此。

 组还可以具有密钥输出，允许打包快捷方式指向有意义的内容。 给定配置中的任何组可能为空，因此不应对组的大小进行假设。 任何配置中每个组的大小（输出数）可能不同于同一配置中另一个组的大小。 它也可能与另一个配置中同一组的大小不同。

 ![输出组图形](../../extensibility/internals/media/vsoutputgroups.gif "vs 输出组")输出组

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg>接口的主要用途是提供生成、部署和调试管理对象的访问，并允许项目自由分组输出。 有关使用此接口的详细信息，请参阅[项目配置对象](../../extensibility/internals/project-configuration-object.md)。

 在上图中，Group Built 具有跨配置（bD.exe 或 b.exe）的关键输出，因此用户可以创建"已建"快捷方式，并且知道无论部署的配置如何，快捷方式都工作。 组源没有密钥输出，因此用户无法创建其快捷方式。 如果调试组"构建"具有密钥输出，但零售组生成没有，则这将是不正确的实现。 因此，如果任何配置具有不包含输出的组，因此没有密钥文件，则具有该组包含输出的其他配置不能具有密钥文件。 安装程序编辑器假定规范名称和组显示名称，加上密钥文件的存在，不会根据配置进行更改。

 请注意，如果项目具有它不想`IVsOutputGroup`打包或部署的 a，则不将该输出放在组中就足够了。 通过实现返回配置的所有输出<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg.EnumOutputs%2A>的方法，无论分组如何，仍可以正常枚举输出。

 有关详细信息，请参阅[项目 MPF](https://github.com/tunnelvisionlabs/MPFProj10)`IVsOutputGroup`的自定义项目示例中的实现。

## <a name="see-also"></a>请参阅
- [管理配置选项](../../extensibility/internals/managing-configuration-options.md)
- [用于生成的项目配置](../../extensibility/internals/project-configuration-for-building.md)
- [项目配置对象](../../extensibility/internals/project-configuration-object.md)
- [解决方案配置](../../extensibility/internals/solution-configuration.md)
