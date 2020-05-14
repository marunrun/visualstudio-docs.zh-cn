---
title: ItemDefinitionGroup 元素 (MSBuild) | Microsoft Docs
ms.date: 03/13/2017
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#ItemDefinitionGroup
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- ItemDefinitionGroup Element [MSBuild]
- <ItemDefinitionGroup> Element [MSBuild]
ms.assetid: 4e9fb04b-5148-4ae5-a394-42861dd62371
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 21e3b6554a9d6e0024cc21fd898962177acfffa7
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "77633624"
---
# <a name="itemdefinitiongroup-element-msbuild"></a>ItemDefinitionGroup 元素 (MSBuild)

使用 `ItemDefinitionGroup` 元素可定义一组项定义，这些项定义默认为应用到项目中的所有项的元数据值。 ItemDefinitionGroup 取代使用 [CreateItem 任务](../msbuild/createitem-task.md)和 [CreateProperty 任务](../msbuild/createproperty-task.md)的需要。 有关详细信息，请参阅[项定义](../msbuild/item-definitions.md)。

\<Project> \<ItemDefinitionGroup>

## <a name="syntax"></a>语法

```xml
<ItemDefinitionGroup Condition="'String A' == 'String B'">
    <Item1>... </Item1>
    <Item2>... </Item2>
</ItemDefinitionGroup>
```

## <a name="attributes-and-elements"></a>特性和元素

下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|特性|描述|
|---------------|-----------------|
|`Condition`|可选特性。 要计算的条件。 有关详细信息，请参阅[条件](../msbuild/msbuild-conditions.md)。|

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|[Item](../msbuild/item-element-msbuild.md)|定义生成过程的输入。 `ItemDefinitionGroup` 中可能没有或有一些 `Item` 元素。|

### <a name="parent-elements"></a>父元素

| 元素 | 描述 |
| - | - |
| [Project](../msbuild/project-element-msbuild.md) | MSBuild 项目文件必需的根元素。 |

## <a name="example"></a>示例

下面的代码示例定义 ItemDefinitionGroup 中的两个元数据项，m 和 n。 在本例中，默认元数据“m”应用于项“i”，这是由于项“i”没有显式定义元数据“m”。 但是，默认元数据“n”无法应用于项“i”，这是由于元数据“n”已经由项“i”定义。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemDefinitionGroup>
        <i>
            <m>m1</m>
            <n>n1</n>
        </i>
    </ItemDefinitionGroup>
    <ItemGroup>
        <i Include="a">
            <o>o1</o>
            <n>n2</n>
        </i>
    </ItemGroup>
    ...
</Project>
```

## <a name="see-also"></a>请参阅

- [项目文件架构参考](../msbuild/msbuild-project-file-schema-reference.md)
- [项](../msbuild/msbuild-items.md)
