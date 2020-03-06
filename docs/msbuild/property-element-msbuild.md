---
title: Property 元素 (MSBuild) | Microsoft Docs
ms.date: 03/13/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- <Property> Element [MSBuild]
- Property Element [MSBuild]
ms.assetid: 69ab08ab-3e76-41dd-a01b-49aa1d2e0cac
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e50a6dd66c2dca7fa4159c578ccd334ed1d26cae
ms.sourcegitcommit: 96737c54162f5fd5c97adef9b2d86ccc660b2135
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/26/2020
ms.locfileid: "77632948"
---
# <a name="property-element-msbuild"></a>Property 元素 (MSBuild)

包含用户定义的属性名和值。 MSBuild 项目中使用的每一个属性都必须指定为 `PropertyGroup` 元素的子元素。

 \<Project> \<PropertyGroup>

## <a name="syntax"></a>语法

```xml
<Property Condition="'String A' == 'String B'">
    Property Value
</Property>
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
|[PropertyGroup](../msbuild/propertygroup-element-msbuild.md)|对属性进行分组。|

## <a name="text-value"></a>文本值

 文本值是可选的。

 此文本指定属性值，并且可能包含 XML。

## <a name="remarks"></a>备注

 属性名称被限制为仅 ASCII 字符。 将属性名放置在“`$(`”和“`)`”之间，从而在项目中引用属性值。 例如，如果 `builddir` 属性具有值 `build`，则 `$(builddir)\classes` 将解析为“build\classes”  。 有关属性的详细信息，请参阅 [MSBuild 属性](../msbuild/msbuild-properties.md)。

## <a name="example"></a>示例

 如果 `Version` 属性为空，那么以下代码会将 `Optimization` 属性设置为 `false`，将 `DefaultVersion` 属性设置为 `1.0`。

```xml
<PropertyGroup>
    <Optimization>false</Optimization>
    <DefaultVersion Condition="'$(Version)' == ''" >1.0</DefaultVersion>
</PropertyGroup>
```

## <a name="see-also"></a>请参阅

- [MSBuild 属性](../msbuild/msbuild-properties.md)
- [项目文件架构参考](../msbuild/msbuild-project-file-schema-reference.md)
