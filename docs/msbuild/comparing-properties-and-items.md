---
title: 比较属性和项 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- msbuild, msbuild properties
ms.assetid: b9da45ae-d6a6-4399-8628-397deed31486
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8217a6aa349a31921ed454e76ddea306785dea9d
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67825905"
---
# <a name="compare-properties-and-items"></a>比较属性和项
MSBuild 属性和项都用于将信息传递给任务、评估条件，以及存储可在整个项目文件中引用的值。

- 属性是名称/值对。 详情请参阅 [MSBuild 属性](../msbuild/msbuild-properties.md)。

- 项是通常表示文件的对象。 项对象具有关联的元数据集合。 元数据是名称/值对。 有关详细信息，请参阅[项](../msbuild/msbuild-items.md)。

## <a name="scalars-and-vectors"></a>标量和矢量
由于 MSBuild 属性是只有一个字符串值的名称/值对，所以它们通常被描述为*标量*。 由于 MSBuild 项类型是项列表，所以它们通常被描述为*矢量*。 但是实际上，属性可以表示多个值，而项类型可以有零个或一个项。

### <a name="target-dependency-injection"></a>目标依赖关系注入
若要查看属性如何表示多个值，请考虑使用常见使用模式将目标添加到要生成的目标列表。 此列表通常由属性值表示，包含用分号分隔的目标名称。

```xml
<PropertyGroup>
    <BuildDependsOn>
        BeforeBuild;
        CoreBuild;
        AfterBuild
    </BuildDependsOn>
</PropertyGroup>
```

`BuildDependsOn` 属性通常用作目标 `DependsOnTargets` 特性的参数，可有效地将该特性转换为项列表。 可以重写此属性，以添加目标或更改目标执行顺序。 例如，应用于对象的

```xml
<PropertyGroup>
    <BuildDependsOn>
        $(BuildDependsOn);
        CustomBuild;
    </BuildDependsOn>
</PropertyGroup>
```

将 CustomBuild 目标添加到目标列表中，为 `BuildDependsOn` 提供值 `BeforeBuild;CoreBuild;AfterBuild;CustomBuild`。

从 MSBuild 4.0 开始，弃用目标依赖关系注入。 改用 `AfterTargets` 和 `BeforeTargets` 特性。 有关详细信息，请参阅[目标生成顺序](../msbuild/target-build-order.md)。

### <a name="conversions-between-strings-and-item-lists"></a>字符串和项列表之间的转换
MSBuild 执行项类型之间的转换，并且需要字符串值。 若要查看项列表如何成为字符串值，请思考项类型用作 MSBuild 属性的值时，会发生什么情况：

```xml
<ItemGroup>
    <OutputDir Include="KeyFiles\;Certificates\" />
</ItemGroup>
<PropertyGroup>
    <OutputDirList>@(OutputDir)</OutputDirList>
</PropertyGroup>
```

项类型 OutputDir 具有值为“KeyFiles\\;Certificates\\”的 `Include` 属性。 MSBuild 将此字符串分析为两项：KeyFiles\ 和 Certificates\\。 当项类型 OutputDir 用作 OutputDirList 属性的值时，MSBuild 会将项类型转换或“平展”到用分号分隔的字符串“KeyFiles\\;Certificates\\”。

## <a name="properties-and-items-in-tasks"></a>任务中的属性和项
对于 MSBuild 任务，属性和项用作输入和输出。 有关详细信息，请参阅[任务](../msbuild/msbuild-tasks.md)。

属性将作为特性传递给任务。 在该任务中，MSBuild 属性由其值可转换为字符串和可由字符串转化得到的属性类型表示。 受支持的属性类型包括 `bool`、`char`、`DateTime`、`Decimal`、`Double`、`int`、`string`，以及任何 <xref:System.Convert.ChangeType%2A> 可以处理的类型。

项作为 <xref:Microsoft.Build.Framework.ITaskItem> 对象传递给任务。 在该任务中，<xref:Microsoft.Build.Framework.ITaskItem.ItemSpec%2A> 表示项的值，<xref:Microsoft.Build.Framework.ITaskItem.GetMetadata%2A> 检索其元数据。

项类型的项列表可以作为 `ITaskItem` 对象的数组传递。 从 .NET Framework 3.5 开始，可以使用 `Remove` 属性将项从目标中的项列表中删除。 因为项可从项列表中删除，所以项类型可能有零个项。 如果项列表传递给任务，则该任务中的代码应该检查这种可能性。

## <a name="property-and-item-evaluation-order"></a>属性和项的计算顺序
在生成的评估阶段期间，已导入的文件将以它们的显示顺序合并到生成中。 按以下顺序，分三个阶段定义属性和项：

- 按照属性的显示顺序，对其进行定义和修改。

- 按照项定义的显示顺序，对其进行定义和修改。

- 按照项的显示顺序，对其进行定义和修改。

在生成的执行阶段期间，在目标内定义的属性和项将以其显示顺序，在一个阶段中进行评估。

但是，此过程并未结束。 在属性、项定义或项被定义后，会计算其值。 表达式计算器将扩展指定值的字符串。 字符串扩展依赖于生成阶段。 以下是更详细的属性和项计算顺序：

- 在生成的评估阶段期间：

  - 按照属性的显示顺序，对其进行定义和修改。 将执行属性函数。 $(PropertyName) 形式的属性值在表达式内扩展。 该属性值设置为已扩展的表达式。

  - 按照项定义的显示顺序，对其进行定义和修改。 属性函数已在表达式内扩展。 元数据值设置为已扩展的表达式。

  - 按照项类型的显示顺序，对其进行定义和修改。 将展开 @(ItemType) 形式的项值。 也会展开项转换。 属性函数和值已在表达式内扩展。 项列表元数据值设置为已扩展的表达式。

- 在生成的执行阶段期间：

  - 在目标内定义的属性和项将以其显示顺序进行评估。 将执行属性函数，并且在表达式内展开属性值。 也会展开项值和项转换。 属性值、项类型值和元数据值设置为已扩展的表达式。

### <a name="subtle-effects-of-the-evaluation-order"></a>计算顺序的细微效果
在生成的评估阶段中，属性计算优先于项计算。 不过，属性可以具有看起来依赖于项值的值。 请考虑使用以下脚本。

```xml
<ItemGroup>
    <KeyFile Include="KeyFile.cs">
        <Version>1.0.0.3</Version>
    </KeyFile>
</ItemGroup>
<PropertyGroup>
    <KeyFileVersion>@(KeyFile->'%(Version)')</KeyFileVersion>
</PropertyGroup>
<Target Name="AfterBuild">
    <Message Text="KeyFileVersion: $(KeyFileVersion)" />
</Target>
```

执行 Message 任务将显示此消息：

```
KeyFileVersion: 1.0.0.3
```

这是因为 `KeyFileVersion` 的值实际是字符串“\@(KeyFile->'%(Version)')”。 第一次定义属性时，项和项转换不会展开，因此 `KeyFileVersion` 属性分配到未扩展字符串的值。

在生成的执行阶段期间，处理 Message 任务时，MSBuild 会将字符串“\@(KeyFile->'%(Version)')”展开到产出“1.0.0.3”中。

请注意，即使属性和项组反向显示，也会出现同一消息。

作为第二个示例，请思考在目标内查找属性和项组时，会发生什么情况：

```xml
<Target Name="AfterBuild">
    <PropertyGroup>
        <KeyFileVersion>@(KeyFile->'%(Version)')</KeyFileVersion>
    </PropertyGroup>
    <ItemGroup>
        <KeyFile Include="KeyFile.cs">
            <Version>1.0.0.3</Version>
        </KeyFile>
    </ItemGroup>
    <Message Text="KeyFileVersion: $(KeyFileVersion)" />
</Target>
```

Message 任务将显示此消息：

```
KeyFileVersion:
```

这是因为在生成的执行阶段期间，将同时自上而下地评估目标内定义的属性和项组。 当 `KeyFileVersion` 得以定义时，`KeyFile` 是未知的。 因此，项转换将展开为空字符串。

在这种情况下，反转属性和项组的顺序将还原原始消息：

```xml
<Target Name="AfterBuild">
    <ItemGroup>
        <KeyFile Include="KeyFile.cs">
            <Version>1.0.0.3</Version>
        </KeyFile>
    </ItemGroup>
    <PropertyGroup>
        <KeyFileVersion>@(KeyFile->'%(Version)')</KeyFileVersion>
    </PropertyGroup>
    <Message Text="KeyFileVersion: $(KeyFileVersion)" />
</Target>
```

`KeyFileVersion` 的值设置为“1.0.0.3”，而非“\@(KeyFile->'%(Version)')”。 Message 任务将显示此消息：

```
KeyFileVersion: 1.0.0.3
```

## <a name="see-also"></a>请参阅
- [高级概念](../msbuild/msbuild-advanced-concepts.md)
