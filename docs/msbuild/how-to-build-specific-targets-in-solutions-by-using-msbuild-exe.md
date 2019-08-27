---
title: 使用 MSBuild.exe 生成解决方案中的特定目标
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, building specific targets in a solution
- msbuild.exe, building specific targets in a solution
- MSBuild, msbuild.exe
ms.assetid: f46feb9b-4c16-4fec-b6e1-36a959692ba3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 34c04d12ccc17424a2f938c04751d4e3d4c9f05f
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/28/2019
ms.locfileid: "66263792"
---
# <a name="how-to-build-specific-targets-in-solutions-by-using-msbuildexe"></a>如何：使用 MSBuild.exe 生成解决方案中的特定目标
可使用 MSBuild 在解决方案中生成特定项目的特定目标。

#### <a name="to-build-a-specific-target-of-a-specific-project-in-a-solution"></a>在解决方案中生成特定项目的特定目标

1. 在命令行中，键入 `MSBuild.exe <SolutionName>.sln`，其中 `<SolutionName>` 对应于包含要执行的目标的解决方案的文件名。

2. 指定 \<ProjectName> 格式的 `-target:` 开关后的目标：\<TargetName>。 如果项目名称包含任何字符 `%`、`$`、`@`、`;`、`.`、`(`、`)` 或 `'`，请将其替换为指定目标名称中的 `_`。

## <a name="example"></a>示例
 以下示例执行 `NotInSlnFolder` 项目的 `Rebuild` 目标，然后执行位于 NewFolder 解决方案文件夹的 `InSolutionFolder` 项目的 `Clean` 目标。

```cmd
msbuild SlnFolders.sln -target:NotInSlnfolder:Rebuild;NewFolder\InSolutionFolder:Clean
```

## <a name="troubleshooting"></a>疑难解答

如果想检查可用选项，可使用 MSBuild 提供的调试选项来执行此操作。 设置环境变量 `MSBUILDEMITSOLUTION=1` 并生成解决方案。 此操作将生成一个名为 \<SolutionName>.sln.metaproj 的 MSBuild 文件，该文件在生成时显示 MSBuild 解决方案的内部视图。 可检查此视图以确定可以生成的目标。

除非需要此内部视图，否则不要使用此环境变量集进行生成操作。 此设置可能会在解决方案中生成项目时导致问题产生。

## <a name="see-also"></a>请参阅
- [命令行参考](../msbuild/msbuild-command-line-reference.md)
- [MSBuild 参考](../msbuild/msbuild-reference.md)
- [MSBuild](../msbuild/msbuild.md)
- [MSBuild 概念](../msbuild/msbuild-concepts.md)
