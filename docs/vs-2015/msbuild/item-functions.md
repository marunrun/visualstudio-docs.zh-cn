---
title: 项函数 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- msbuild, Item functions
ms.assetid: 5e6df3cc-2db8-4cbd-8fdd-3ffd03ac0876
caps.latest.revision: 32
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c94624aaea629c087b552ee46266a44f534888d5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68192894"
---
# <a name="item-functions"></a>项函数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

从 MSBuild 4.0 开始，任务和目标中的代码可以调用项函数来获取项目中各项的相关信息。 这些函数简化 Distinct() 项的获取过程，并且比循环遍历项的速度更快。  
  
## <a name="string-item-functions"></a>字符串项函数  
 可以在 .NET Framework 中使用字符串方法和属性对任何项值进行操作。 对于 <xref:System.String> 方法，指定方法名称。 对于 <xref:System.String> 属性，请在“get_”之后指定属性名。  
  
 对于具有多个字符串的项，字符串方法或属性会对每个字符串运行。  
  
 下面的示例显示如何使用这些字符串项函数。  
  
```  
<ItemGroup>  
    <theItem Include="andromeda;tadpole;cartwheel" />  
</ItemGroup>  
  
<Target Name = "go">  
    <Message Text="IndexOf  @(theItem->IndexOf('r'))" />  
    <Message Text="Replace  @(theItem->Replace('tadpole', 'pinwheel'))" />  
    <Message Text="Length   @(theItem->get_Length())" />  
    <Message Text="Chars    @(theItem->get_Chars(2))" />  
</Target>  
  
  <!--  
  Output:  
    IndexOf  3;-1;2  
    Replace  andromeda;pinwheel;cartwheel  
    Length   9;7;9  
    Chars    d;d;r  
  -->  
```  
  
## <a name="intrinsic-item-functions"></a>内部项函数  
 下表列出了可用于各项的内部函数。  
  
|函数|示例|说明|  
|--------------|-------------|-----------------|  
|`Count`|`@(MyItem->Count())`|返回项计数。|  
|`DirectoryName`|`@(MyItem->DirectoryName())`|返回每个项的 `Path.DirectoryName` 等效项。|  
|`Distinct`|`@(MyItem->Distinct())`|返回具有不同 `Include` 值的项。 忽略元数据。 比较不区分大小写。|  
|`DistinctWithCase`|`@(MyItem->DistinctWithCase())`|返回具有不同 `itemspec` 值的项。 忽略元数据。 比较是区分大小写的。|  
|`Reverse`|`@(MyItem->Reverse())`|按相反顺序返回项。|  
|`AnyHaveMetadataValue`|`@(MyItem->AnyHaveMetadataValue("MetadataName", "MetadataValue"))`|返回 `boolean`，指示是否有任何项具有给定的元数据名和值。 比较不区分大小写。|  
|`ClearMetadata`|`@(MyItem->ClearMetadata())`|返回清除了元数据的项。 仅保留 `itemspec`。|  
|`HasMetadata`|`@(MyItem->HasMetadataValue("MetadataName")`|返回具有给定元数据名的项。 比较不区分大小写。|  
|`Metadata`|`@(MyItem->Metadata("MetadataName"))`|返回具有元数据名的元数据的值。|  
|`WithMetadataValue`|`@(MyItem->WithMetadataValue("MetadataName", "MetadataValue")`|返回具有给定元数据名和值的项。 比较不区分大小写。|  
  
 下面的示例显示如何使用内部项函数。  
  
```  
<ItemGroup>  
    <TheItem Include="first">  
        <Plant>geranium</Plant>  
    </TheItem>  
    <TheItem Include="second">  
        <Plant>algae</Plant>  
    </TheItem>  
    <TheItem Include="third">  
        <Plant>geranium</Plant>  
    </TheItem>  
</ItemGroup>  
  
<Target Name="go">  
    <Message Text="MetaData:    @(TheItem->Metadata('Plant'))" />  
    <Message Text="HasMetadata: @(theItem->HasMetadata('Plant'))" />  
    <Message Text="WithMetadataValue: @(TheItem->WithMetadataValue('Plant', 'geranium'))" />  
    <Message Text=" " />  
    <Message Text="Count:   @(theItem->Count())" />  
    <Message Text="Reverse: @(theItem->Reverse())" />  
</Target>  
  
  <!--   
  Output:  
    MetaData:    geranium;algae;geranium  
    HasMetadata: first;second;third  
    WithMetadataValue: first;third  
  
    Count:   3  
    Reverse: third;second;first  
  -->  
```  
  
## <a name="see-also"></a>另请参阅  
 [项](../msbuild/msbuild-items.md)
