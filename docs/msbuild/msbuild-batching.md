---
title: MSBuild 批处理 | Microsoft Docs
ms.date: 06/09/2020
ms.topic: conceptual
helpviewer_keywords:
- batching [MSBuild]
- MSBuild, batching
ms.assetid: d35c085b-27b8-49d7-b6f8-8f2f3a0eec38
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6d7c72d1da270220144cd5e6167ebecb66462ba9
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85289269"
---
# <a name="msbuild-batching"></a>MSBuild 批处理

MSBuild 根据项元数据将项列表划分为不同的类别或批，并对每批一次运行一个目标或任务。

## <a name="task-batching"></a>任务批处理

借助任务批处理，可以用某种方式将项列表划分为不同批次，同时将每个批次单独地传递到任务中来简化项目文件。 这意味着项目文件只需要声明一次任务及其特性就可多次运行该任务。

通过在任务特性之一中使用 `%(ItemMetaDataName)` 表示法，指定希望 MSBuild 对任务执行批处理。 以下示例基于 `Color` 项元数据值将 `Example` 项列表划分为几个批次，并将每个批次单独地传递到 `MyTask` 任务。

> [!NOTE]
> 如果没有在任务特性中的其他位置引用项列表，或者如果元数据名称可能不明确，则可以使用 %(<ItemCollection.ItemMetaDataName>) 表示法来完全限定要用于批处理的项元数据值。

```xml
<Project
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <ItemGroup>
        <Example Include="Item1">
            <Color>Blue</Color>
        </Example>
        <Example Include="Item2">
            <Color>Red</Color>
        </Example>
    </ItemGroup>

    <Target Name="RunMyTask">
        <MyTask
            Sources = "@(Example)"
            Output = "%(Color)\MyFile.txt"/>
    </Target>

</Project>
```

有关更具体的批处理示例，请参阅[任务批处理中的项元数据](../msbuild/item-metadata-in-task-batching.md)。

## <a name="target-batching"></a>目标批处理

MSBuild 先检查目标的输入和输出是否是最新的，再运行目标。 如果输入和输出都是最新的，则跳过目标。 如果目标内的任务使用批处理，则 MSBuild 需要确定每批项的输入和输出是否是最新的。 否则，目标将在每次命中时执行。

以下示例展示了包含使用 `%(ItemMetadataName)` 表示法的 `Outputs` 特性的 `Target` 元素。 MSBuild 会基于 `Color` 项元数据将 `Example` 项列表划分为几个批次，并分析每个批次的输出文件的时间戳。 如果批处理的输出不是最新的，则运行目标。 否则，跳过该目标。

```xml
<Project
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <ItemGroup>
        <Example Include="Item1">
            <Color>Blue</Color>
        </Example>
        <Example Include="Item2">
            <Color>Red</Color>
        </Example>
    </ItemGroup>

    <Target Name="RunMyTask"
        Inputs="@(Example)"
        Outputs="%(Color)\MyFile.txt">
        <MyTask
            Sources = "@(Example)"
            Output = "%(Color)\MyFile.txt"/>
    </Target>

</Project>
```

有关目标批处理的另一个示例，请参阅[目标批处理中的项元数据](../msbuild/item-metadata-in-target-batching.md)。

## <a name="item-and-property-mutations"></a>项和属性突变

此部分介绍了在使用目标批处理或任务批处理时，如何理解更改属性和/或项元数据的影响。

由于目标批处理和任务批处理是两种不同的 MSBuild 操作，因此请务必确切了解在每种情况下 MSBuild 使用哪种形式的批处理。 如果批处理语法 `%(ItemMetadataName)` 出现在目标内的任务中，但没有出现在目标特性中，则 MSBuild 使用任务批处理。 指定目标批处理的唯一方法是，对目标特性（通常是 `Outputs` 特性）使用批处理语法。

对于目标批处理和任务批处理，可以认为批处理是独立运行的。 所有批处理都从复制处于相同初始状态的属性和项元数据值开始。 批处理执行期间的任何属性值突变对其他批处理都不可见。 请看下面的示例：

```xml
  <ItemGroup>
    <Thing Include="2" Color="blue" />
    <Thing Include="1" Color="red" />
  </ItemGroup>

  <Target Name="DemoIndependentBatches">
    <ItemGroup>
      <Thing Condition=" '%(Color)' == 'blue' ">
        <Color>red</Color>
        <NeededColorChange>true</NeededColorChange>
      </Thing>
    </ItemGroup>
    <Message Importance="high"
             Text="Things: @(Thing->'%(Identity) is %(Color); needed change=%(NeededColorChange)')"/>
  </Target>
```

输出为：

```output
Target DemoIndependentBatches:
  Things: 2 is red; needed change=true;1 is red; needed change=
```

目标中的 `ItemGroup` 是一项隐式任务，借助 `Condition` 特性中的 `%(Color)`，执行的是任务批处理。 有两个批处理：一个用于红色，另一个用于蓝色。 只有在 `%(Color)` 元数据为 blue 时，才设置属性 `%(NeededColorChange)`，并且此设置只影响在运行蓝色批处理时与条件匹配的单个项。 尽管有 `%(ItemMetadataName)` 语法，`Message` 任务的 `Text` 特性也不会触发批处理，因为是在项转换内使用了它。

批处理单独运行，而不是并行运行。 当你访问在批处理执行中更改的元数据值时，这就会产生差异。 如果设置基于批处理执行中的某元数据的属性，则此属性接受最后设置的值：

```xml
   <PropertyGroup>
       <SomeProperty>%(SomeItem.MetadataValue)</SomeProperty>
   </PropertyGroup>
```

在批处理执行后，此属性保留 `%(MetadataValue)` 的最终值。

尽管批处理是独立运行的，但也请务必注意目标批处理与任务批处理之间的区别，并知道哪种类型适用于你的情况。 请参阅以下示例，以更好地理解这种区别的重要性。

任务可以是隐式的，而不是显式的，当对隐式任务执行任务批处理时，这可能会令人困惑。 当 `Target` 中出现 `PropertyGroup` 或 `ItemGroup` 元素时，组中的每个属性声明都会得到隐式处理，有点像独立的 [CreateProperty](createproperty-task.md) 或 [CreateItem](createitem-task.md) 任务。 也就是说，对目标执行批处理和不执行批处理（即 `Outputs` 特性中缺少 `%(ItemMetadataName)` 语法）时的行为是不同的。 如果对目标执行批处理，`ItemGroup` 每目标执行一次，但如果对目标不执行批处理，就会使用任务批处理对 `CreateItem` 或 `CreateProperty` 任务的隐式等效项进行批处理，所以目标只执行一次，并且组中的每个项或属性都使用任务批处理分别进行批处理。

下面的示例演示了在元数据突变时的目标批处理与任务批处理。 假设你在文件夹 A 和 B 中有一些文件：

```
A\1.stub
B\2.stub
B\3.stub
```

现在看看这两个类似项目的输出。

```xml
    <ItemGroup>
      <StubFiles Include="$(MSBuildThisFileDirectory)**\*.stub"/>

      <StubDirs Include="@(StubFiles->'%(RecursiveDir)')"/>
    </ItemGroup>

    <Target Name="Test1" AfterTargets="Build" Outputs="%(StubDirs.Identity)">
      <PropertyGroup>
        <ComponentDir>%(StubDirs.Identity)</ComponentDir>
        <ComponentName>$(ComponentDir.TrimEnd('\'))</ComponentName>
      </PropertyGroup>

      <Message Text=">> %(StubDirs.Identity) '$(ComponentDir)' '$(ComponentName)'"/>
    </Target>
```

输出为：

```output
Test1:
  >> A\ 'A\' 'A'
Test1:
  >> B\ 'B\' 'B'
```

现在删除指定了目标批处理的 `Outputs` 特性。

```xml
    <ItemGroup>
      <StubFiles Include="$(MSBuildThisFileDirectory)**\*.stub"/>

      <StubDirs Include="@(StubFiles->'%(RecursiveDir)')"/>
    </ItemGroup>

    <Target Name="Test1" AfterTargets="Build">
      <PropertyGroup>
        <ComponentDir>%(StubDirs.Identity)</ComponentDir>
        <ComponentName>$(ComponentDir.TrimEnd('\'))</ComponentName>
      </PropertyGroup>

      <Message Text=">> %(StubDirs.Identity) '$(ComponentDir)' '$(ComponentName)'"/>
    </Target>
```

输出为：

```output
Test1:
  >> A\ 'B\' 'B'
  >> B\ 'B\' 'B'
```

我们注意到，标题 `Test1` 只打印了一次，但是在上一个示例中，它打印了两次。 也就是说，目标未进行批处理。  因此，输出是不同的，且令人困惑。

原因在于，在使用目标批处理时，每个目标批处理都使用自己的独立副本（其中包含所有属性和项）来执行目标中的所有内容，但如果省略 `Outputs` 特性，属性组中的各个行就会被视为可能已批处理的不同任务。 在此示例中，批处理的是 `ComponentDir` 任务（它使用 `%(ItemMetadataName)` 语法），这样在 `ComponentName` 行执行时，`ComponentDir` 行的两个批处理都已完成，并且运行的第二个批处理确定了第二行中所示的值。

## <a name="property-functions-using-metadata"></a>使用元数据的属性函数

可通过包括元数据的属性函数控制批处理。 例如，应用于对象的

`$([System.IO.Path]::Combine($(RootPath),%(Compile.Identity)))`

使用 <xref:System.IO.Path.Combine%2A> 合并根文件夹路径与编译项路径。

属性函数可能不会出现在元数据值内。 例如，应用于对象的

`%(Compile.FullPath.Substring(0,3))`

是不允许的。

有关属性函数详细信息，请参阅[属性函数](../msbuild/property-functions.md)。

## <a name="see-also"></a>请参阅

- [ItemMetadata 元素 (MSBuild)](../msbuild/itemmetadata-element-msbuild.md)
- [MSBuild 概念](../msbuild/msbuild-concepts.md)
- [MSBuild 参考](../msbuild/msbuild-reference.md)
- [高级概念](../msbuild/msbuild-advanced-concepts.md)
