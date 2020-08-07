---
title: MSBuild 中的解决方案筛选器
description: 介绍解决方案筛选器并演示如何使用 MSBuild 生成解决方案筛选器文件。
ms.date: 07/28/2020
ms.topic: reference
helpviewer_keywords:
- MSBuild, solution filters
- solution filters [MSBuild]
author: ghogen
ms.author: ghogen
manager: jillfra
monikerRange: '>= vs-2019'
ms.openlocfilehash: 998103828d20827e8a1d99e0cc34d7f9beb6bd7c
ms.sourcegitcommit: 9179c33a78c2ac690ce908d7c73eef50b6e367f0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/29/2020
ms.locfileid: "87401043"
---
# <a name="solution-filters-in-msbuild"></a>MSBuild 中的解决方案筛选器

解决方案筛选器文件是扩展名为 .slnf 的 JSON 文件，用于指示要从解决方案中的所有项目生成或加载的项目。 从 MSBuild 16.7 开始，可以对解决方案筛选器文件调用 MSBuild，以生成启用了筛选功能的解决方案。 

> [!NOTE]
> 解决方案筛选器文件减少了要加载或生成的项目集，并简化了格式。 解决方案文件仍然是必需的。

## <a name="build-a-solution-filter-from-the-command-line"></a>从命令行生成解决方案筛选器

从命令行生成解决方案筛选器文件的操作使用与生成解决方案文件完全相同的语法。 指定解决方案筛选器文件而不是要生成的启用了筛选功能的解决方案，如下所示：

```console
msbuild [options] solutionFilterFile.slnf
```

还可以像往常一样追加开关和额外的属性。 请参阅 [MSBuild 命令行参考](msbuild-command-line-reference.md)。 此命令生成筛选的项目及其依赖的任何项目。 在从命令行生成解决方案筛选器时，MSBuild 会自动遵循依赖关系。 如果在筛选器中指定或由生成的项目引用，则它会生成项目。

## <a name="solution-filter-files"></a>解决方案筛选器文件

可以使用 Visual Studio 来处理解决方案筛选器文件。 在 Visual Studio 中打开解决方案筛选器将显示卸载的项目和加载的项目，并提供加载更多项目以选择生成的选项。 还可以加载初始项目依赖其生成的所有项目，但这不是必需的。 请参阅[筛选的解决方案](../ide/filtered-solutions.md)。

解决方案筛选器不必与解决方案在同一文件夹中。 解决方案文件的路径相对于解决方案筛选器文件的位置，而每个项目的路径相对于解决方案文件本身，并且应与解决方案文件中的项目路径匹配。 下面的示例演示相对路径的用法：

```json
{
  "solution": {
    "path": "..\\..\\Documents\\GitHub\\msbuild\\MSBuild.sln",
    "projects": [
      "src\\Build.OM.UnitTests\\Microsoft.Build.Engine.OM.UnitTests.csproj"
    ]
  }
}
```

路径中的反斜杠必须成对出现，因为它们经过转义。

## <a name="example"></a>示例

下面是 Visual Studio 中筛选的解决方案的一个示例：

![Visual Studio 中筛选的解决方案的屏幕截图](media/solution-with-filter.png)

在此解决方案中，ClassLibrary1 由 ProjectA 和 ProjectB 使用，因此 ClassLibrary1 作为项目引用列出。

下面是 Visual Studio 生成的解决方案筛选器文件：

```json
{
  "solution": {
    "path": "MyApplication.sln",
    "projects": [
      "MyApplication\\MyApplication.csproj",
      "ProjectA\\ProjectA.csproj"
    ]
  }
}
```

在此示例中，当你生成启用了筛选功能的解决方案时（通过 `MSBuild [options] MyFilter.slnf` 命令），MSBuild 将生成 MyApplication 和 ProjectA，因为它们在解决方案筛选器文件中显式列出。 在生成 ProjectA 的过程中，MSBuild 将生成 ClassLibrary1，因为 ProjectA 依赖于它。  不会生成 ProjectB。 （此讨论假设一个干净生成。 如果以前生成了项目，则常用规则适用于跳过最新的项目。）

## <a name="see-also"></a>请参阅

- [筛选的解决方案](../ide/filtered-solutions.md)
- [MSBuild 命令行参考](msbuild-command-line-reference.md)
