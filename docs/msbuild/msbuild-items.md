---
title: MSBuild 项 | Microsoft Docs
description: 使用 ItemGroup 的 MSBuild Include 属性指定要包含在生成中的文件
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, Items
ms.assetid: d762eff4-c92a-4b5f-a944-1ca30aa22319
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a8ed6b9789569e9f68706a5b132aa9000b25d910
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75590639"
---
# <a name="msbuild-items"></a>MSBuild 项
MSBuild 项是生成系统的输入，通常表示文件（文件在 `Include` 属性中指定）。 根据项元素名称，将其组成不同的项类型。 项类型是项的命名列表，可用作任务参数。 任务使用项值来执行生成过程。

 由于项是根据其所属项类型命名，因此术语“项”和“项值”可互换使用。

## <a name="create-items-in-a-project-file"></a>在项目文件中创建项
 声明项目文件中的项为 [ItemGroup](../msbuild/itemgroup-element-msbuild.md) 元素的子元素。 子元素的名称是项的类型。 该元素的 `Include` 属性指定该项类型要包含的项（文件）。 例如，下面的 XML 会创建一个名为 `Compile` 的项类型，其中包括两个文件。

```xml
<ItemGroup>
    <Compile Include = "file1.cs"/>
    <Compile Include = "file2.cs"/>
</ItemGroup>
```

 项“file2.cs”不会替换项“file1.cs”；相反，将在 `Compile` 项类型的值列表中追加该文件名   。

 以下 XML 通过在一个 `Include` 属性中声明两个文件，创建相同的项类型。 请注意，文件名由分号分隔。

```xml
<ItemGroup>
    <Compile Include = "file1.cs;file2.cs"/>
</ItemGroup>
```

## <a name="create-items-during-execution"></a>在执行过程中创建项
 在生成的评估阶段会为 [Target](../msbuild/target-element-msbuild.md) 元素外的项分配值。 在后续执行阶段中，可通过以下方式创建或修改项：

- 任何任务都可以发出项。 若要发出项，[Task](../msbuild/task-element-msbuild.md) 元素必须具有含有 `ItemName` 属性的 [Output](../msbuild/output-element-msbuild.md) 子元素。

- [CreateItem](../msbuild/createitem-task.md) 任务可发出项。 此用法已弃用。

- 从 .NET Framework 3.5 起，`Target` 元素可能会包含 [ItemGroup](../msbuild/itemgroup-element-msbuild.md) 元素，后者可能会包含项元素。

## <a name="reference-items-in-a-project-file"></a>在项目文件中引用项
 若要在整个项目文件中引用项类型，请使用语法 @(\<ItemType>)。 例如，使用 `@(Compile)` 引用前面示例中的项类型。 使用此语法，将项类型指定为该任务的参数，从而将项传递到任务。 有关详细信息，请参阅[如何：选择要生成的文件](../msbuild/how-to-select-the-files-to-build.md)。

 默认情况下，项类型的项展开时由分号 (;) 分隔。 可使用语法 @(\<ItemType>, '\<separator>') 指定非默认分隔符。 有关详细信息，请参阅[如何：显示用逗号分隔的项列表](../msbuild/how-to-display-an-item-list-separated-with-commas.md)。

## <a name="use-wildcards-to-specify-items"></a>使用通配符指定项

可使用 `**`、`*` 和 `?` 通配符，将一组文件指定为生成项目的输入，而不用单独列出每个文件。

- `?` 通配符匹配单个字符。
- `*` 通配符匹配零个或多个字符。
- `**` 通配符序列匹配部分路径。

例如，可以在项目文件中使用下列元素，以在包含项目文件的目录中指定所有 `.cs` 文件。

```xml
<CSFile Include="*.cs"/>
```

下列元素选择 `D:` 驱动器上的所有 `.vb` 文件：

```xml
<VBFile Include="D:/**/*.vb"/>
```

若要在项中添加 `*` 或 `?` 文本字符，而不进行通配符扩展，必须[转义通配符](../msbuild/how-to-escape-special-characters-in-msbuild.md)。

有关通配符的详细信息，请参阅[如何：选择要生成的文件](../msbuild/how-to-select-the-files-to-build.md)。

## <a name="use-the-exclude-attribute"></a>使用 Exclude 属性
 项元素可包含 `Exclude` 属性，该属性用于从项类型中排除特定项（文件）。 `Exclude` 属性通常与通配符一起使用。 例如，除 DoNotBuild.cs 文件外，以下 XML 将目录中的每个 .cs 文件都添加到 CSFile 项类型   。

```xml
<ItemGroup>
    <CSFile  Include="*.cs"  Exclude="DoNotBuild.cs"/>
</ItemGroup>
```

 `Exclude` 属性只会影响同时包含这两种属性的项目文件中由 `Include` 属性添加的项。 以下示例不会排除在之前的项元素中添加的文件 Form1.cs  。

```xml
<Compile Include="*.cs" />
<Compile Include="*.res" Exclude="Form1.cs">
```

 有关详细信息，请参阅[如何：从生成中排除文件](../msbuild/how-to-exclude-files-from-the-build.md)。

## <a name="item-metadata"></a>项元数据
 除 `Include` 和 `Exclude` 属性中的信息外，项可能还包含元数据。 对于需要关于项的详细信息的任务，或需对任务和目标进行批处理的任务，可使用元数据。 有关详细信息，请参阅[批处理](../msbuild/msbuild-batching.md)。

 元数据是键值对集合，其在项目文件中声明为项元素的子元素。 子元素的名称是元数据的名称，且子元素的值是元数据的值。

 元数据与包含它的项元素相关联。 例如，以下 XML 将具有值 `Fr` 的元数据 `Culture` 添加到 CSFile 项类型的 “one.cs”和“one.cs”项   。

```xml
<ItemGroup>
    <CSFile Include="one.cs;two.cs">
        <Culture>Fr</Culture>
    </CSFile>
</ItemGroup>
```

 项可以有零个或零个以上的元数据值。 可随时更改元数据值。 如果将元数据设置为空值，则可有效将其从生成中删除。

### <a name="BKMK_ReferencingItemMetadata"></a>在项目文件中引用项元数据
 可使用语法 %(\<ItemMetadataName>)，在整个项目中引用项元数据。 如果存在不明确性，则可使用项类型的名称来限定引用。 例如，可指定 %(\<ItemType.ItemMetaDataName>)。以下示例使用 Display 元数据对 Message 任务进行批处理。 若要深入了解如何使用项元数据进行批处理，请参阅[任务批处理中的项元数据](../msbuild/item-metadata-in-task-batching.md)。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup>
        <Stuff Include="One.cs" >
            <Display>false</Display>
        </Stuff>
        <Stuff Include="Two.cs">
            <Display>true</Display>
        </Stuff>
    </ItemGroup>
    <Target Name="Batching">
        <Message Text="@(Stuff)" Condition=" '%(Display)' == 'true' "/>
    </Target>
</Project>
```

### <a name="BKMK_WellKnownItemMetadata"></a>常见项元数据
 向项类型添加项时，会向该项分配一些常见元数据。 例如，所有项都具有常见元数据 %(\<Filename>)，其值是项的文件名。 有关详细信息，请参阅[常见项元数据](../msbuild/msbuild-well-known-item-metadata.md)。

### <a name="BKMK_Transforming"></a>使用元数据转换项类型
 通过使用元数据，可将项列表转换为新的项列表。 例如，可使用 `@(CppFiles -> '%(Filename).obj')` 表达式将含有表示 .cpp 文件的项的项类型 `CppFiles` 转换为相应的 .obj 文件列表   。

 以下代码创建 `CultureResource` 项类型，其中含有所有带 `Culture` 元数据的 `EmbeddedResource` 项的副本。 `Culture` 元数据值将成为新的 `CultureResource.TargetDirectory` 元数据的值。

```xml
<Target Name="ProcessCultureResources">
    <ItemGroup>
        <CultureResource Include="@(EmbeddedResource)"
            Condition="'%(EmbeddedResource.Culture)' != ''">
            <TargetDirectory>%(EmbeddedResource.Culture) </TargetDirectory>
        </CultureResource>
    </ItemGroup>
</Target>
```

 有关详细信息，请参阅[转换](../msbuild/msbuild-transforms.md)。

## <a name="item-definitions"></a>项定义
 从.NET Framework 3.5 起，即可使用 [ItemDefinitionGroup 元素](../msbuild/itemdefinitiongroup-element-msbuild.md)向任何项类型添加默认元数据。 与已知元数据一样，默认元数据与指定项类型的所有项关联。 可在项定义中显式重写默认元数据。 例如，下面的 XML 向 `Compile` 项“one.cs”和“three.cs”提供值为“Monday”的 `BuildDay` 元数据   。 代码会向“two.cs”项提供值为“Tuesday”的 `BuildDay` 元数据  。

```xml
<ItemDefinitionGroup>
    <Compile>
        <BuildDay>Monday</BuildDay>
    </Compile>
</ItemDefinitionGroup>
<ItemGroup>
    <Compile Include="one.cs;three.cs" />
    <Compile Include="two.cs">
        <BuildDay>Tuesday</BuildDay>
    </Compile>
</ItemGroup>
```

 有关详细信息，请参阅[项定义](../msbuild/item-definitions.md)。

## <a name="attributes-for-items-in-an-itemgroup-of-a-target"></a>目标的 ItemGroup 中项的属性
 从 .NET Framework 3.5 起，`Target` 元素可能会包含 [ItemGroup](../msbuild/itemgroup-element-msbuild.md) 元素，后者可能会包含项元素。 为 `Target` 中 `ItemGroup` 内的项指定此部分中属性时，该属性有效。

### <a name="BKMK_RemoveAttribute"></a>删除属性
 `Remove` 属性从项类型中删除特定项（文件）。 此属性是在 .NET Framework 3.5 中推出的（仅限内部目标）。 从 MSBuild 15.0 开始，同时支持内部和外部目标。

 以下示例从 Compile 项类型删除所有 .config 文件  。

```xml
<Target>
    <ItemGroup>
        <Compile Remove="*.config"/>
    </ItemGroup>
</Target>
```

### <a name="BKMK_KeepMetadata"></a>KeepMetadata 属性
 如果项在目标中生成，则项元素中会包含 `KeepMetadata` 属性。 如果指定了此属性，则只会将在由分号分隔的名称列表中指定的元数据从源项传输到目标项。 若此属性为空值，相当于不进行指定。 `KeepMetadata` 属性是在 .NET Framework 4.5 中引入的。

 以下示例介绍如何使用 `KeepMetadata` 属性。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003"
ToolsVersion="4.0">

    <ItemGroup>
        <FirstItem Include="rhinoceros">
            <Class>mammal</Class>
            <Size>large</Size>
        </FirstItem>

    </ItemGroup>
    <Target Name="MyTarget">
        <ItemGroup>
            <SecondItem Include="@(FirstItem)" KeepMetadata="Class" />
        </ItemGroup>

        <Message Text="FirstItem: %(FirstItem.Identity)" />
        <Message Text="  Class: %(FirstItem.Class)" />
        <Message Text="  Size:  %(FirstItem.Size)"  />

        <Message Text="SecondItem: %(SecondItem.Identity)" />
        <Message Text="  Class: %(SecondItem.Class)" />
        <Message Text="  Size:  %(SecondItem.Size)"  />
    </Target>
</Project>

<!--
Output:
  FirstItem: rhinoceros
    Class: mammal
    Size:  large
  SecondItem: rhinoceros
    Class: mammal
    Size:
-->
```

### <a name="BKMK_RemoveMetadata"></a>RemoveMetadata 属性
 如果项在目标中生成，则项元素中会包含 `RemoveMetadata` 属性。 如果指定了此属性，则除包含在由分号分隔的名称列表中的元数据外，会将所有元数据从源项传输到目标项。 若此属性为空值，相当于不进行指定。 `RemoveMetadata` 属性是在 .NET Framework 4.5 中引入的。

 以下示例介绍如何使用 `RemoveMetadata` 属性。

```xml
<Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>
        <MetadataToRemove>Size;Material</MetadataToRemove>
    </PropertyGroup>

    <ItemGroup>
        <Item1 Include="stapler">
            <Size>medium</Size>
            <Color>black</Color>
            <Material>plastic</Material>
        </Item1>
    </ItemGroup>

    <Target Name="MyTarget">
        <ItemGroup>
            <Item2 Include="@(Item1)" RemoveMetadata="$(MetadataToRemove)" />
        </ItemGroup>

        <Message Text="Item1: %(Item1.Identity)" />
        <Message Text="  Size:     %(Item1.Size)" />
        <Message Text="  Color:    %(Item1.Color)" />
        <Message Text="  Material: %(Item1.Material)" />
        <Message Text="Item2: %(Item2.Identity)" />
        <Message Text="  Size:     %(Item2.Size)" />
        <Message Text="  Color:    %(Item2.Color)" />
        <Message Text="  Material: %(Item2.Material)" />
    </Target>
</Project>

<!--
Output:
  Item1: stapler
    Size:     medium
    Color:    black
    Material: plastic
  Item2: stapler
    Size:
    Color:    black
    Material:
-->
```

### <a name="BKMK_KeepDuplicates"></a>KeepDuplicates 属性
 如果项在目标中生成，则项元素中会包含 `KeepDuplicates` 属性。 `KeepDuplicates` 是一个 `Boolean` 属性，当项是现有项的完全相同的副本时，该属性可指定是否应将该项添加到目标组中。

 如果源项和目标项的 Include 值相同，但元数据不同，那么即使将 `KeepDuplicates` 设为 `false` 仍会添加项。 若此属性为空值，相当于不进行指定。 `KeepDuplicates` 属性是在 .NET Framework 4.5 中引入的。

 以下示例介绍如何使用 `KeepDuplicates` 属性。

```xml
<Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <ItemGroup>
        <Item1 Include="hourglass;boomerang" />
        <Item2 Include="hourglass;boomerang" />
    </ItemGroup>

    <Target Name="MyTarget">
        <ItemGroup>
            <Item1 Include="hourglass" KeepDuplicates="false" />
            <Item2 Include="hourglass" />
        </ItemGroup>

        <Message Text="Item1: @(Item1)" />
        <Message Text="  %(Item1.Identity)  Count: @(Item1->Count())" />
        <Message Text="Item2: @(Item2)" />
        <Message Text="  %(Item2.Identity)  Count: @(Item2->Count())" />
    </Target>
</Project>

<!--
Output:
  Item1: hourglass;boomerang
    hourglass  Count: 1
    boomerang  Count: 1
  Item2: hourglass;boomerang;hourglass
    hourglass  Count: 2
    boomerang  Count: 1
-->
```

## <a name="see-also"></a>请参阅
- [Item 元素 (MSBuild)](../msbuild/item-element-msbuild.md)
- [常用的 MSBuild 项目项](../msbuild/common-msbuild-project-items.md)
- [MSBuild 概念](../msbuild/msbuild-concepts.md)
- [MSBuild](../msbuild/msbuild.md)
- [如何：选择要生成的文件](../msbuild/how-to-select-the-files-to-build.md)
- [如何：从生成中排除文件](../msbuild/how-to-exclude-files-from-the-build.md)
- [如何：显示用逗号分隔的项列表](../msbuild/how-to-display-an-item-list-separated-with-commas.md)
- [项定义](../msbuild/item-definitions.md)
- [批处理](../msbuild/msbuild-batching.md)
