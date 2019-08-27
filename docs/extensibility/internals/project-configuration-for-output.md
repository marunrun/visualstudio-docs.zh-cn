---
title: 项目配置为输出 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project configurations, output
ms.assetid: a4517f73-45af-4745-9d7f-9fddf887b636
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5f1fa63a0e3143be6f8133b2a8ae3a57fe6857a9
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66328384"
---
# <a name="project-configuration-for-output"></a>用于输出的项目配置
每一种配置可以支持一组生成输出项，如可执行文件或资源文件的生成进程。 这些输出项专用于用户，并可以放入链接的输出，例如可执行文件 （.exe、.dll、.lib） 和源文件 （.idl、.h 文件） 的相关的类型的组。

 输出项便可通过提供<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutput2>方法和枚举与<xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumOutputs>方法。 当你想向输出项进行分组时，你的项目还应实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputGroup>接口。

 通过实现开发构造`IVsOutputGroup`允许到组根据使用情况的输出的项目。 例如，一个 DLL 可能与其程序数据库 (PDB) 进行分组。

> [!NOTE]
> PDB 文件包含调试信息并生成.dll 或.exe 时指定生成调试信息选项时创建它。 为仅调试项目配置通常生成.pdb 文件。

 项目必须返回相同数量的支持，每个配置的组，即使的组中包含的输出数可能会配置配置有所不同。 例如，项目 Matt 的 DLL 可能会在调试配置中，包括 mattd.dll 和 mattd.pdb 但仅在零售配置中包括 matt.dll。

 组之间还具有相同的标识符信息，如规范名称、 显示名称和组信息，请配置配置项目中。 这种一致性允许部署和打包以继续运行，即使配置更改。

 组还可以允许打包快捷方式以指向有意义的名称的一个主要输出。 任何组可能在给定配置中，为空，因此应有关组的大小不进行任何假设。 每个组中的任何配置的大小 （多个输出） 可以不同于在相同的配置中的另一个组的大小。 它还可以从另一种配置中的相同组的大小不同。

 ![输出组图](../../extensibility/internals/media/vsoutputgroups.gif "vsOutputGroups")输出组

 主要用途<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg>接口是为了提供访问以生成、 部署和调试管理对象并允许到组的输出可以自由的项目。 使用此接口的详细信息，请参阅[项目配置对象](../../extensibility/internals/project-configuration-object.md)。

 在上图中，组生成都有一个键，因此输出配置 （bD.exe 或 b.exe） 中用户可以创建内置的快捷方式和知道该快捷方式，将正常工作而不考虑部署的配置。 组源没有输出，一个密钥，因此用户不能创建它的快捷方式。 如果调试组生成有主要输出，但零售组生成没有的将是实现不正确。 下述，然后，如果任何配置有不包含任何输出，一个组，并没有密钥的文件，然后与该组包含输出的其他配置操作结果，不能具有密钥文件。 安装程序编辑器假定规范名称和显示名称的组，以及存在一个密钥文件，不要更改基于在配置中。

 请注意，如果一个项目具有`IVsOutputGroup`，它不希望以打包或部署，就足以将该输出放在组中。 输出仍可枚举通常通过实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg.EnumOutputs%2A>返回所有配置的输出，而不考虑分组的方法。

 有关详细信息，请参阅的实现`IVsOutputGroup`中的自定义项目示例[项目的 MPF](https://github.com/tunnelvisionlabs/MPFProj10)。

## <a name="see-also"></a>请参阅
- [管理配置选项](../../extensibility/internals/managing-configuration-options.md)
- [用于生成的项目配置](../../extensibility/internals/project-configuration-for-building.md)
- [项目配置对象](../../extensibility/internals/project-configuration-object.md)
- [解决方案配置](../../extensibility/internals/solution-configuration.md)