---
title: Target 元素 (MSBuild) | Microsoft Docs
ms.date: 06/13/2019
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Target
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Target element [MSBuild]
- <Target> element [MSBuild]
ms.assetid: 350f6fc2-86b3-45f2-a31e-ece0e6bd4dca
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 79686132adce043b4864d545f0912564709cfe2c
ms.sourcegitcommit: 96737c54162f5fd5c97adef9b2d86ccc660b2135
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/26/2020
ms.locfileid: "77631973"
---
# <a name="target-element-msbuild"></a>Target 元素 (MSBuild)

包含一组要连续执行的 MSBuild 任务。

 \<Project> \<Target>

## <a name="syntax"></a>语法

```xml
<Target Name="Target Name"
        Inputs="Inputs"
        Outputs="Outputs"
        Returns="Returns"
        KeepDuplicateOutputs="true/false"
        BeforeTargets="Targets"
        AfterTargets="Targets"
        DependsOnTargets="DependentTarget"
        Condition="'String A' == 'String B'"
        Label="Label">
    <Task>... </Task>
    <PropertyGroup>... </PropertyGroup>
    <ItemGroup>... </ItemGroup>
    <OnError... />
</Target>
```

## <a name="attributes-and-elements"></a>特性和元素

 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|`Name`|必需的特性。<br /><br /> 目标的名称。|
|`Condition`|可选特性。<br /><br /> 要评估的条件。 如果该条件评估结果为 `false`，那么目标不会执行目标主体或任何在 `DependsOnTargets` 属性中设置的目标。 有关条件的详细信息，请参阅[条件](../msbuild/msbuild-conditions.md)。|
|`Inputs`|可选特性。<br /><br /> 形成此目标输入的文件。 采用分号分隔多个文件。 将会比较该文件的时间戳与 `Outputs` 中文件的时间戳，从而确定 `Target` 是否为最新。 有关详细信息，请参阅[增量生成](../msbuild/incremental-builds.md)、[如何：增量生成](../msbuild/how-to-build-incrementally.md)以及[转换](../msbuild/msbuild-transforms.md)。|
|`Outputs`|可选特性。<br /><br /> 形成此目标输出的文件。 采用分号分隔多个文件。 将会比较该文件的时间戳与 `Inputs` 中文件的时间戳，从而确定 `Target` 是否为最新。 有关详细信息，请参阅[增量生成](../msbuild/incremental-builds.md)、[如何：增量生成](../msbuild/how-to-build-incrementally.md)以及[转换](../msbuild/msbuild-transforms.md)。|
|`Returns`|可选特性。<br /><br /> 一组可供调用此目标（例如，MSBuild 任务）的任务使用的项。 采用分号分隔多个目标。 如果该文件中的目标没有 `Returns` 属性，则会使用输出属性来实现此目的。|
|`KeepDuplicateOutputs`|可选布尔属性。<br /><br /> 如果为 `true`，则会记录对目标的“返回”中的同一项的多个引用。  默认情况下，此属性为 `false`。|
|`BeforeTargets`|可选特性。<br /><br /> 分号分隔的目标名称列表。  指定时，表示此目标应在指定的一个或多个目标之前运行。 这样项目作者就可以扩展现有的一组目标，而无需直接对其进行修改。 有关详细信息，请参阅[目标生成顺序](../msbuild/target-build-order.md)。|
|`AfterTargets`|可选特性。<br /><br /> 分号分隔的目标名称列表。 指定时，表示此目标应在指定的一个或多个目标之后运行。 这样项目作者就可以扩展现有的一组目标，而无需直接对其进行修改。 有关详细信息，请参阅[目标生成顺序](../msbuild/target-build-order.md)。|
|`DependsOnTargets`|可选特性。<br /><br /> 必须先执行该目标，才能执行此目标或开始顶级依赖关系分析。 采用分号分隔多个目标。|
|`Label`|可选特性。<br /><br /> 可标识系统和用户元素或对其进行排序的标识符。|

### <a name="child-elements"></a>子元素

| 元素 | 描述 |
| - | - |
| [Task](../msbuild/task-element-msbuild.md) | 创建并执行的 MSBuild 任务的实例。 目标中可能有零个或零个以上的任务。 |
| [PropertyGroup](../msbuild/propertygroup-element-msbuild.md) | 包含一组用户定义的 `Property` 元素。 自 .NET Framework 3.5 起，`Target` 元素可能包含 `PropertyGroup` 元素。 |
| [ItemGroup](../msbuild/itemgroup-element-msbuild.md) | 包含一组用户定义的 `Item` 元素。 自 .NET Framework 3.5 起，`Target` 元素可能包含 `ItemGroup` 元素。 有关详细信息，请参阅[项](../msbuild/msbuild-items.md)。 |
| [OnError](../msbuild/onerror-element-msbuild.md) | 对于失败的任务，如果 `ContinueOnError` 属性为 ErrorAndStop（或 `false`），则会出现一个或多个要执行的任务。 目标中可能有零个或零个以上的 `OnError` 元素。 如果存在 `OnError` 元素，则其必须为 `Target` 元素中最后的元素。<br /><br /> 有关 `ContinueOnError` 属性的详细信息，请参阅 [Task 元素 (MSBuild)](../msbuild/task-element-msbuild.md)。 |

### <a name="parent-elements"></a>父元素

| 元素 | 描述 |
| - | - |
| [Project](../msbuild/project-element-msbuild.md) | MSBuild 项目文件必需的根元素。 |

## <a name="remarks"></a>备注

 在运行时指定第一个要执行的目标。 目标可依赖于其他目标。 例如，部署的目标依赖于编译的目标。 MSBuild 引擎按依赖关系在 `DependsOnTargets` 属性中出现的顺序从左到右依次执行依赖关系。 有关详细信息，请参阅[目标](../msbuild/msbuild-targets.md)。

 MSBuild 依赖于导入顺序，带有特定 `Name` 属性的目标的最后一个定义是使用的定义。

 即使一个目标与多个目标存在依赖关系，在生成过程中该目标也只执行一次。

 如果因为目标 `Condition` 属性的评估结果为 `false` 而跳过了该目标，那么稍后在生成中调用该目标时，仍可执行该目标且此时其 `Condition` 属性评估结果为 `true`。

 在 MSBuild 4 之前，`Target` 会返回 `Outputs` 属性中指定的所有项。  为实现此目的，MSBuild 就必须记录这些项，以防稍后生成中的任务会需要这些项。 由于无法表明哪些目标含有调用方请求的输出，因此 MSBuild 将所有调用的 `Target` 上所有 `Outputs` 的所有项汇集到了一起。 这为含有大量输出项的生成带来了缩放问题。

 如果用户在项目中的任何 `Target` 元素上指定 `Returns`，则只有含有 `Returns` 属性的那些 `Target` 会记录这些项。

 `Target` 可能包含 `Outputs` 属性和 `Returns` 属性。  `Outputs` 与 `Inputs` 一起确定目标是否为最新目标。 如果存在 `Returns`，则替代 `Outputs` 的值，从而确定要返回给调用方的项。  如果不存在 `Returns`，则提供 `Outputs` 供调用方使用，但之前描述的情况除外。

 在 MSBuild 4 之前，只要 `Target` 的 `Outputs` 中包含对同一项的多个引用，就会记录这些副本项。 在含有许多输出和许多项目相互依赖项的各种大型生成中，这会浪费大量的内存，因为副本项没有任何用处。 将 `KeepDuplicateOutputs` 属性设置为 `true` 时，就会记录这些副本。

## <a name="example"></a>示例

 以下代码示例演示执行 `Csc` 任务的 `Target` 元素。

```xml
<Target Name="Compile" DependsOnTargets="Resources" Returns="$(TargetPath)">
    <Csc Sources="@(CSFile)"
          TargetType="library"
          Resources="@(CompiledResources)"
          EmitDebugInformation="$(includeDebugInformation)"
          References="@(Reference)"
          DebugType="$(debuggingType)" >
        <Output TaskParameter="OutputAssembly"
                  ItemName="FinalAssemblyName" />
    </Csc>
</Target>
```

## <a name="see-also"></a>请参阅

- [目标](../msbuild/msbuild-targets.md)
- [项目文件架构参考](../msbuild/msbuild-project-file-schema-reference.md)
