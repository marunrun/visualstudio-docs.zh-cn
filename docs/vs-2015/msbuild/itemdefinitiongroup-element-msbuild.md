---
title: ItemDefinitionGroup 元素 (MSBuild) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
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
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b5aea9c7c7868dfdd9726b86bb344456ebe707d8
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68162440"
---
# <a name="itemdefinitiongroup-element-msbuild"></a>ItemDefinitionGroup 元素 (MSBuild)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用 `ItemDefinitionGroup` 元素可定义一组项定义，这些项定义默认为应用到项目中的所有项的元数据值。 ItemDefinitionGroup 取代使用 [CreateItem 任务](../msbuild/createitem-task.md)和 [CreateProperty 任务](../msbuild/createproperty-task.md)的需要。 有关详细信息，请参阅[项定义](../msbuild/item-definitions.md)。  
  
 \<Project>  
 \<ItemDefinitionGroup>  
  
## <a name="syntax"></a>语法  
  
```  
<ItemGroup Condition="'String A' == 'String B'">  
    <Item1>... </Item1>  
    <Item2>... </Item2>  
</ItemGroup>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|说明|  
|---------------|-----------------|  
|`Condition`|可选特性。 要计算的条件。 有关详细信息，请参阅[条件](../msbuild/msbuild-conditions.md)。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|说明|  
|-------------|-----------------|  
|[Item](../msbuild/item-element-msbuild.md)|定义生成过程的输入。 `ItemDefinitionGroup` 中可能没有或有一些 `Item` 元素。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|说明|  
|-------------|-----------------|  
|[Project](../msbuild/project-element-msbuild.md)|[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 项目文件必需的根元素。|  
  
## <a name="example"></a>示例  
 下面的代码示例定义 ItemDefinitionGroup 中的两个元数据项，m 和 n。 在本例中，默认元数据“m”应用于项“i”，这是由于项“i”没有显式定义元数据“m”。 但是，默认元数据“n”无法应用于项“i”，这是由于元数据“n”已经由项“i”定义。  
  
```  
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
  
## <a name="see-also"></a>另请参阅  
 [项目文件架构参考](../msbuild/msbuild-project-file-schema-reference.md)   
 [项](../msbuild/msbuild-items.md)
