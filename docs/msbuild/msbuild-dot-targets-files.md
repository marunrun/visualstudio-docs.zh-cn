---
title: MSBuild .targets 文件 | Microsoft Docs
ms.date: 02/24/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- .targets files
- MSBuild, .targets files
ms.assetid: f6d98eb4-d2fa-49b7-8e3c-bae1ca3cf596
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4dc5df9c4eba4195400b6a41fa50a5c88257d70e
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75566548"
---
# <a name="msbuild-targets-files"></a>MSBuild .targets 文件
[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 包括多个 .targets 文件，文件内容包含常见方案的项、属性、目标和任务  。 这些文件将自动导入到大多数 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 项目文件中，以便简化维护，增强可读性。

 项目通常会导入一个或多个 .targets 文件以定义它们的生成进程  。 例如由 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 创建的 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] 项目将导入 Microsoft.CSharp.targets，它可导入 Microsoft.Common.targets   。 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] 项目本身会定义特定于该项目的项和属性，但 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] 项目的标准生成规则在导入的 .targets 文件中进行定义  。

 `$(MSBuildToolsPath)` 值指定这些公用 .targets 文件的路径  。 如果 `ToolsVersion` 为 4.0，则文件位于以下位置： *\<WindowsInstallationPath>\Microsoft.NET\Framework\v4.0.30319\\*

> [!NOTE]
> 若要了解如何创建自己的目标，请参阅[目标](../msbuild/msbuild-targets.md)。 有关如何使用 `Import` 元素将项目文件插入到其他项目文件的详细信息，请参阅 [Import 元素 (MSBuild)](../msbuild/import-element-msbuild.md) 和[如何：在多个项目文件中使用同一目标](../msbuild/how-to-use-the-same-target-in-multiple-project-files.md)。

## <a name="common-targets-files"></a>公用 .targets 文件

| .targets 文件  | 描述 |
|---------------------------------| - |
| *Microsoft.Common.targets* | 定义 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 和 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] 项目标准生成过程中的步骤。<br /><br /> 由 Microsoft.CSharp.targets 和 Microsoft.VisualBasic.targets 文件导入，其中包括以下语句：`<Import Project="Microsoft.Common.targets" />`   |
| *Microsoft.CSharp.targets* | 定义 Visual C# 项目标准生成过程中的步骤。<br /><br /> 由 Visual C# 项目文件 (.csproj) 导入，其中包括以下语句：`<Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />`  |
| *Microsoft.VisualBasic.targets* | 定义 Visual Basic 项目标准生成过程中的步骤。<br /><br /> 由 Visual Basic 项目文件 (.vbproj) 导入，其中包括以下语句：`<Import Project="$(MSBuildToolsPath)\Microsoft.VisualBasic.targets" />`  |

## <a name="directorybuildtargets"></a>Directory.Build.targets
Directory.Build.targets 是用户定义的对目录下的项目提供自定义选项的文件  。 除非属性 ImportDirectoryBuildTargets 设为 false，否则该文件将从 Microsoft.Common.targets 自动导入    。 有关详细信息，请参阅[自定义生成](customize-your-build.md)。

## <a name="see-also"></a>请参阅
- [Import 元素 (MSBuild)](../msbuild/import-element-msbuild.md)
- [MSBuild 参考](../msbuild/msbuild-reference.md)
- [MSBuild](../msbuild/msbuild.md)
