---
title: 目标生成顺序 | Microsoft Docs
ms.date: 05/02/2019
ms.topic: conceptual
helpviewer_keywords:
- msbuild, build order
ms.assetid: f4a26339-9f9a-497a-9aa6-0797183d450d
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 607584b4b41bdfde224bdb35d30eec1c6c8a4197
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75585452"
---
# <a name="target-build-order"></a>目标生成顺序

如果目标的输入取决于另一目标的输出，那么必须将目标排序。 可使用这些属性指定目标运行的顺序：

- `InitialTargets`。 `Project` 属性指定将首先运行的目标，即使在命令行或 `DefaultTargets` 属性中指定了目标。

- `DefaultTargets`。 如果未在命令行上显示指定目标，则此 `Project` 属性可指定要运行的目标。

- `DependsOnTargets`。 此 `Target` 属性指定必须运行的目标后才能运行此目标。

- `BeforeTargets` 和 `AfterTargets`。 这些 `Target` 属性指定应在指定的目标运行前或后 (MSBuild 4.0) 运行此目标。

生成过程中一个目标绝不会运行两次，即使在生成中有后续目标依赖于该目标。 目标运行后，其在生成中的任务就已完成。

目标可能有 `Condition` 属性。 如果指定的条件评估结果为 `false`，那么该目标不会执行且对生成没有影响。 有关条件的详细信息，请参阅[条件](../msbuild/msbuild-conditions.md)。

## <a name="initial-targets"></a>初始目标

`InitialTargets`Project[ 元素的 ](../msbuild/project-element-msbuild.md) 属性指定将首先运行的目标，即使在命令行或 `DefaultTargets` 属性中指定了目标。 初始目标常用于错误检查。

`InitialTargets` 属性的值可以是以分号分隔的、有序的目标列表。 以下示例指定运行的 `Warm` 目标，然后指定运行的 `Eject` 目标。

```xml
<Project InitialTargets="Warm;Eject" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
```

导入的项目可能有自己的 `InitialTargets` 属性。 所有初始目标都聚集在一起并按顺序运行。

有关详细信息，请参阅[如何：指定首先生成的目标](../msbuild/how-to-specify-which-target-to-build-first.md)。

## <a name="default-targets"></a>默认目标

如果未在命令行上显式指定某个目标，`DefaultTargets`Project[ 元素的 ](../msbuild/project-element-msbuild.md) 属性可指定将生成哪个或哪些目标。

`DefaultTargets` 属性的值可以是以分号分隔的、有序的默认目标列表。 以下示例指定运行的 `Clean` 目标，然后指定运行的 `Build` 目标。

```xml
<Project DefaultTargets="Clean;Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
```

若要重写默认目标，可以在命令行中使用 -target  开关。 以下示例指定运行的 `Build` 目标，然后指定运行的 `Report` 目标。 以此方式指定目标时，将忽略所有默认目标。

 `msbuild -target:Build;Report`

如果指定了初始目标和默认目标，且未指定命令行的目标，那么 MSBuild 会先运行初始目标，然后运行默认目标。

导入的项目可能有自己的 `DefaultTargets` 属性。 第一个出现的 `DefaultTargets` 属性将确定要运行的默认目标。

有关详细信息，请参阅[如何：指定首先生成的目标](../msbuild/how-to-specify-which-target-to-build-first.md)。

## <a name="first-target"></a>第一个目标

如果没有初始目标、默认目标或命令行目标，那么 MSBuild 会先运行项目文件中或任意导入的项目文件中出现的第一个目标。

## <a name="target-dependencies"></a>目标依赖项

目标可描述相互依赖关系。 `DependsOnTargets` 属性表示目标依赖于其他目标。 例如，应用于对象的

```xml
<Target Name="Serve" DependsOnTargets="Chop;Cook" />
```

告知 MSBuild `Serve` 目标依赖于 `Chop` 目标和 `Cook` 目标。 MSBuild 将运行 `Chop` 目标，然后运行 `Cook` 目标，之后再运行 `Serve` 目标。

## <a name="beforetargets-and-aftertargets"></a>在目标之前和在目标之后

在 MSBuild 4.0 中，可通过使用 `BeforeTargets` 和 `AfterTargets` 属性指定目标顺序。

请考虑使用以下脚本。

```xml
<Project DefaultTargets="Compile;Link" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <Target Name="Compile">
        <Message Text="Compiling" />
    </Target>
    <Target Name="Link">
        <Message Text="Linking" />
    </Target>
</Project>
```

若要创建在 `Optimize` 目标后，`Compile` 目标前运行的直接目标 `Link`，请将以下目标添加到 `Project` 元素中的任意位置。

```xml
<Target Name="Optimize"
    AfterTargets="Compile" BeforeTargets="Link">
    <Message Text="Optimizing" />
</Target>
```

## <a name="determine-the-target-build-order"></a>确定目标生成顺序

MSBuild 按以下方式确定目标生成顺序：

1. 运行 `InitialTargets` 目标。

2. 运行的是在命令行中使用 -target  开关指定的目标。 如果未在命令行上指定目标，则运行 `DefaultTargets` 目标。 如果都不存在，则运行出现的第一个目标。

3. 评估目标的 `Condition` 属性。 如果出现 `Condition` 属性且评估结果为 `false`，那么不会运行该目标，且目标不会对生成造成进一步影响。

   列出 `BeforeTargets` 或 `AfterTargets` 中的条件目标的其他目标仍按指定顺序执行。

4. 在执行或跳过目标之前，将运行其 `DependsOnTargets` 目标，除非将 `Condition` 属性应用于目标并且计算结果为 `false`。

   > [!NOTE]
   > 如果目标未执行，则会将其视为已跳过，因为其输出项是最新的（请参阅[增量生成](../msbuild/incremental-builds.md)）。 此检查在执行目标内的任务之前完成，并且不会影响目标的执行顺序。

5. 执行或跳过目标之前，运行 `BeforeTargets` 属性中列出的目标的其他目标。

6. 执行目标前，会比较其 `Inputs` 属性和 `Outputs` 属性。 如果 MSBuild 确定任何输出文件相对于相应的输入文件过期，那么 MSBuild 将执行该目标。 否则，MSBuild 会跳过该目标。

7. 执行或跳过目标后，运行 `AfterTargets` 属性中列出目标的任何其他目标。

## <a name="see-also"></a>另请参阅

- [目标](../msbuild/msbuild-targets.md)
