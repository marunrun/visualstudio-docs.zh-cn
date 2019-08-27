---
title: Property 元素 (MSBuild) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- <Property> Element [MSBuild]
- Property Element [MSBuild]
ms.assetid: 69ab08ab-3e76-41dd-a01b-49aa1d2e0cac
caps.latest.revision: 20
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: eefe0160328f1eb6b3fe841742547efe8be50ec1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68158265"
---
# <a name="property-element-msbuild"></a>Property 元素 (MSBuild)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

包含用户定义的属性名和值。 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 项目中使用的每一个属性都必须被指定为 `PropertyGroup` 元素的子元素。  
  
 \<Project>  
 \<PropertyGroup>  
  
## <a name="syntax"></a>语法  
  
```  
<Property Condition="'String A' == 'String B'">  
    Property Value  
</Property>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|说明|  
|---------------|-----------------|  
|`Condition`|可选特性。<br /><br /> 要计算的条件。 有关详细信息，请参阅[条件](../msbuild/msbuild-conditions.md)。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|说明|  
|-------------|-----------------|  
|[PropertyGroup](../msbuild/propertygroup-element-msbuild.md)|对属性进行分组。|  
  
## <a name="text-value"></a>文本值  
 文本值是可选的。  
  
 此文本指定属性值，并且可能包含 XML。  
  
## <a name="remarks"></a>备注  
 属性名称被限制为仅 ASCII 字符。 将属性名放置在“`$(`”和“`)`”之间，从而在项目中引用属性值。 例如，如果 `builddir` 属性具有值 `build`，则 `$(builddir)\classes` 将解析为“build\classes”。 有关属性的详细信息，请参阅 [MSBuild 属性](msbuild-properties1.md)。  
  
## <a name="example"></a>示例  
 如果 `Version` 属性为空，那么以下代码会将 `Optimization` 属性设置为 `false`，将 `DefaultVersion` 属性设置为 `1.0`。  
  
```  
<PropertyGroup>  
    <Optimization>false</Optimization>  
    <DefaultVersion Condition="'$(Version)' == ''" >1.0</DefaultVersion>  
</PropertyGroup>  
```  
  
## <a name="see-also"></a>另请参阅
[MSBuild 属性](msbuild-properties1.md)  
 [项目文件架构参考](../msbuild/msbuild-project-file-schema-reference.md)
