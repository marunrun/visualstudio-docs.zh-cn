---
title: Item 元素 (MSBuild) | Microsoft Docs
ms.date: 03/13/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Item Element [MSBuild]
- <Item> Element [MSBuild]
ms.assetid: dcef5f91-0613-4bfc-8ee9-d7004bb6d3a9
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ff7e446c319a08004260125580cdace43412cdba
ms.sourcegitcommit: 1efb6b219ade7c35068b79fbdc573a8771ac608d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2020
ms.locfileid: "78169347"
---
# <a name="item-element-msbuild"></a>Item 元素 (MSBuild)

包含用户定义的项和其元数据。 MSBuild 项目中使用的每一个项都必须被指定为 `ItemGroup` 元素的子元素。

\<Project> \<ItemGroup> \<Item>

## <a name="syntax"></a>语法

```xml
<Item Include="*.cs"
        Exclude="MyFile.cs"
        Condition="'String A'=='String B'">
    <ItemMetadata1>...</ItemMetadata1>
    <ItemMetadata2>...</ItemMetadata2>
</Item>
```

## <a name="specify-metadata-as-attributes"></a>指定元数据作为属性

在 MSBuild 15.1 或更高版本中，名称不与当前属性列表冲突的元数据可选择性地表示为属性。

例如，若要指定 NuGet 包列表，你通常会使用类似下列语法的内容。

```xml
<ItemGroup>
  <PackageReference Include="Newtonsoft.Json">
    <Version>9.0.1-beta1<Version>
  </PackageReference>
</ItemGroup>
```

但是，现在你可以传递 `Version` 元数据作为属性，如下列语法所示：

```xml
<ItemGroup>
  <PackageReference Include="Newtonsoft.Json" Version="9.0.1-beta1" />
</ItemGroup>
```

## <a name="attributes-and-elements"></a>特性和元素

 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|`Include`|可选特性。<br /><br /> 项列表中要包含的文件或通配符。|
|`Exclude`|可选特性。<br /><br /> 项列表中要排除的文件或通配符。|
|`Condition`|可选特性。<br /><br /> 要评估的条件。 有关详细信息，请参阅[条件](../msbuild/msbuild-conditions.md)。|
|`Remove`|可选特性。<br /><br /> 要从项列表中删除的文件或通配符。<br /><br />|
|`KeepDuplicates`|可选特性。<br /><br /> 指定如果项是现有项的完全相同的副本时是否应将该项添加到目标组中。 如果源项和目标项的 `Include` 值相同但元数据不同，那么即使将 `KeepDuplicates` 设为`false` 仍会添加项。 有关详细信息，请参阅[项](../msbuild/msbuild-items.md)。<br /><br /> 仅当为位于 `ItemGroup` 内的 `Target` 中的项指定该属性时，该属性才有效。|
|`KeepMetadata`|可选特性。<br /><br /> 要添加到目标项的源项的元数据。 只有在以分号分隔的列表中指定了名称的元数据会从源项传输到目标项。 有关详细信息，请参阅[项](../msbuild/msbuild-items.md)。<br /><br /> 仅当为位于 `ItemGroup` 内的 `Target` 中的项指定该属性时，该属性才有效。|
|`RemoveMetadata`|可选特性。<br /><br /> 不传输到目标项的源项的元数据。 所有元数据都会从源项传输到目标项，名称被列在以分号分隔的名称列表中的元数据除外。 有关详细信息，请参阅[项](../msbuild/msbuild-items.md)。<br /><br /> 仅当为位于 `ItemGroup` 内的 `Target` 中的项指定该属性时，该属性才有效。|
|`Update`|可选特性。 （仅适用于 Visual Studio 2017 或更高版本中的 .NET Core 项目。）<br /><br /> 使你可以修改使用 glob 包含的文件的元数据。<br /><br /> 仅当为不存在于 `Target` 内的 `ItemGroup` 中的项指定该属性时，该属性才有效。|

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|[ItemMetadata](../msbuild/itemmetadata-element-msbuild.md)|用户定义的包含项元数据值的项元数据键。 项中可能没有或有一些 `ItemMetadata` 元素。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[ItemGroup](../msbuild/itemgroup-element-msbuild.md)|为项进行元素分组。|

## <a name="remarks"></a>备注

`Item` 元素定义输入到生成系统的输入，并且根据其用户定义的集合名被分组到项集合。 这些项集合可用作[任务](../msbuild/msbuild-tasks.md)的参数，这些任务使用集合中的各个项来执行生成过程的步骤。 有关详细信息，请参阅[项](../msbuild/msbuild-items.md)。

使用表示法 @(\<myType>) 可使类型 \<myType> 的项的集合扩展为以分号分隔的字符串列表，并将传递给参数。 如果参数的类型为 `string`，则参数的值是以分号分隔的元素列表。 如果此参数是一个字符串数组 (`string[]`)，则根据分号的位置将每个元素插入到数组中。 如果任务参数的类型为 <xref:Microsoft.Build.Framework.ITaskItem>`[]`，则值是项集合的内容以及附加的任何元数据。 如需通过使用分号之外的其他字符来分隔每个项，请使用语法 @(\<myType>, '\<separator>')。

MSBuild 引擎能够计算通配符（如 `*` 和 `?`）和递归通配符（如 /\*\*/\*.cs  ）。 有关详细信息，请参阅[项](../msbuild/msbuild-items.md)。

## <a name="examples"></a>示例

以下代码示例演示如何声明类型 `CSFile` 的两个项。 第二个声明项包含将 `MyMetadata` 设置为 `HelloWorld` 的元数据。

```xml
<ItemGroup>
    <CSFile Include="engine.cs; form.cs" />
    <CSFile Include="main.cs" >
        <MyMetadata>HelloWorld</MyMetadata>
    </CSFile>
</ItemGroup>
```

以下代码示例演示如何使用 `Update` 属性修改通过 glob 包含的 somefile.cs 文件中的元数据  。 （仅适用于 Visual Studio 2017 或更高版本中的 .NET Core 项目。）

```xml
<ItemGroup>
    <Compile Update="somefile.cs">  // or Update="*.designer.cs"
        <MetadataKey>MetadataValue</MetadataKey>
    </Compile>
</ItemGroup>
```

## <a name="see-also"></a>请参阅

- [项](../msbuild/msbuild-items.md)
- [常用的 MSBuild 项目项](../msbuild/common-msbuild-project-items.md)
- [MSBuild 属性](../msbuild/msbuild-properties.md)
- [项目文件架构参考](../msbuild/msbuild-project-file-schema-reference.md)
