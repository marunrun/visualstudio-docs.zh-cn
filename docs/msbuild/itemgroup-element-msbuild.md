---
title: ItemGroup 元素 (MSBuild) | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#ItemGroup
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- ItemGroup element [MSBuild]
- <ItemGroup> element [MSBuild]
ms.assetid: aac894e3-a9f1-4bbc-a796-6ef07001f35b
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a62b4df06d1c180a6a6d62b0231dce1136fb8059
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85288970"
---
# <a name="itemgroup-element-msbuild"></a>ItemGroup 元素 (MSBuild)

包含一组用户定义的 [Item](../msbuild/item-element-msbuild.md) 元素。 MSBuild 项目中使用的每一个项都必须被指定为 `ItemGroup` 元素的子元素。

\<Project>
\<ItemGroup>

## <a name="syntax"></a>语法

```xml
<ItemGroup Condition="'String A' == 'String B'"
           Label="Label">
    <Item1>... </Item1>
    <Item2>... </Item2>
</ItemGroup>
```

## <a name="attributes-and-elements"></a>特性和元素

下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|`Condition`|可选特性。 要计算的条件。 有关详细信息，请参阅[条件](../msbuild/msbuild-conditions.md)。|
|`Label`|可选特性。 标识 `ItemGroup`。 |

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|[Item](../msbuild/item-element-msbuild.md)|定义生成过程的输入。 `ItemGroup` 中可能没有或有一些 `Item` 元素。|

### <a name="parent-elements"></a>父元素

| 元素 | 描述 |
| - | - |
| [Project](../msbuild/project-element-msbuild.md) | MSBuild 项目文件必需的根元素。 |
| [Target](../msbuild/target-element-msbuild.md) | 从 .NET Framework 3.5 开始，`ItemGroup` 元素可以出现在 `Target` 元素内部。 有关详细信息，请参阅[目标](../msbuild/msbuild-targets.md)。 |

## <a name="example"></a>示例

以下代码示例演示用户定义的项集合 `Res` 和 `ItemGroup` 元素内部声明的 `CodeFiles`。 `Res` 项集合中的每个项均包含用户定义的子 [ItemMetadata](../msbuild/itemmetadata-element-msbuild.md) 元素。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup>
        <Res Include = "Strings.fr.resources" >
            <Culture>fr</Culture>
        </Res>
        <Res Include = "Dialogs.fr.resources" >
            <Culture>fr</Culture>
        </Res>

        <CodeFiles Include="**\*.cs" Exclude="**\generated\*.cs" />
        <CodeFiles Include="..\..\Resources\Constants.cs" />
    </ItemGroup>
...
</Project>
```

在简单的项目文件中，通常使用单个 `ItemGroup` 元素，但也可以使用多个 `ItemGroup` 元素。 当使用多个 `ItemGroup` 元素时，多个项会合并为单个 `ItemGroup`。 例如，某些项可能包含在导入文件中定义的单独 `ItemGroup` 元素中。

ItemGroups 可以通过使用 `Condition` 属性来应用条件。 在这种情况下，仅当满足条件时才会将项添加到项列表。 请参阅 [MSBuild 条件](msbuild-conditions.md)

`Label` 属性在某些生成系统中用作控制生成行为的方式。 只能在声明中使用它，作为创建更易于理解的 MSBuild 脚本的一种方法，或作为影响生成操作的控件设置。

## <a name="see-also"></a>请参阅

- [项目文件架构参考](../msbuild/msbuild-project-file-schema-reference.md)
- [项](../msbuild/msbuild-items.md)
- [常用的 MSBuild 项目项](../msbuild/common-msbuild-project-items.md)
