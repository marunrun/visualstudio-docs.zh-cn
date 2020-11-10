---
title: ImportGroup 元素 | Microsoft Docs
description: 了解 MSBuild 如何使用 ImportGroup 元素来包含分组到可选条件下的一批 Import 元素。
ms.custom: SEO-VS-2020
ms.date: 03/13/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- <ImportGroup> element [MSBuild]
- ImportGroup element [MSBuild]
ms.assetid: dac3fa2d-6678-4017-af35-93686f53f302
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 865ee2b319cc3cd26f6924110fa2976f526ac4f4
ms.sourcegitcommit: f1d47655974a2f08e69704a9a0c46cb007e51589
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92903942"
---
# <a name="importgroup-element"></a>ImportGroup 元素

  
包含在可选条件下进行分组的 `Import` 元素的集合。 有关详细信息，请参阅 [Import 元素 (MSBuild)](../msbuild/import-element-msbuild.md)。

```xml
<Project>
  <ImportGroup>
```

## <a name="syntax"></a>语法

```xml
<ImportGroup Condition="'String A' == 'String B'">
    <Import ... />
    <Import ... />
</ImportGroup>
```

## <a name="attributes-and-elements"></a>特性和元素

 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|描述|
|---------------|-----------------|
|`Condition`|可选特性。<br /><br /> 要评估的条件。 有关详细信息，请参阅[条件](../msbuild/msbuild-conditions.md)。|

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|[导入](../msbuild/import-element-msbuild.md)|将一个项目文件的内容导入其他项目文件中。|

### <a name="parent-elements"></a>父元素

| 元素 | 描述 |
| - | - |
| [Project](../msbuild/project-element-msbuild.md) | MSBuild 项目文件必需的根元素。 |

## <a name="example"></a>示例

 以下代码示例演示 `ImportGroup` 元素。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ImportGroup>
        <Import Project="$(Targets1.targets)" />
        <Import Project="$(Targets2.targets)" />
    </ImportGroup>
...
</Project>
```

## <a name="see-also"></a>请参阅

- [项目文件架构参考](../msbuild/msbuild-project-file-schema-reference.md)
- [项](../msbuild/msbuild-items.md)
