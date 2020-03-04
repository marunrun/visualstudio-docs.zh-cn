---
title: ItemMetadata 元素 (MSBuild) | Microsoft Docs
ms.date: 03/13/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- ItemMetadata Element [MSBuild]
- <ItemMetadata> Element [MSBuild]
ms.assetid: e3db5122-202d-43a9-b2f4-3e0ec4ed3d08
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 18e1722fcd6867ca5e8ae52e220ff0a3dd2a3b7f
ms.sourcegitcommit: 96737c54162f5fd5c97adef9b2d86ccc660b2135
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/26/2020
ms.locfileid: "77633611"
---
# <a name="itemmetadata-element-msbuild"></a>ItemMetadata 元素 (MSBuild)

包含用户定义的项元数据键，其中包含项元数据值。 一个项可能具有任意数量的元数据键值对。

 \<Project> \<ItemGroup> \<Item>

## <a name="syntax"></a>语法

```xml
<ItemMetadataName> Item Metadata value</ItemMetadataName>
```

## <a name="attributes-and-elements"></a>特性和元素

 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|`Condition`|可选特性。<br /><br /> 要计算的条件。 有关详细信息，请参阅[条件](../msbuild/msbuild-conditions.md)。|

### <a name="child-elements"></a>子元素

 无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[Item](../msbuild/item-element-msbuild.md)|为生成过程定义输入的用户定义元素。|

## <a name="text-value"></a>文本值

 文本值是可选的。

 此文本指定项元数据值可以是文本，也可以是 XML。

## <a name="example"></a>示例

 下面的代码示例演示如何将具有值 `fr` 的 `Culture` 元数据添加到项 `CSFile`。

```xml
<ItemGroup>
    <CSFile Include="main.cs" >
        <Culture>fr</Culture>
    </CSFile>
</ItemGroup>
```

## <a name="see-also"></a>请参阅

- [项目文件架构参考](../msbuild/msbuild-project-file-schema-reference.md)
- [项](../msbuild/msbuild-items.md)
