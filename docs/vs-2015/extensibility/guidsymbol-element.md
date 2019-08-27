---
title: GuidSymbol 元素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- VSCT XML schema elements, GuidSymbol
- GuidSymbol element (VSCT XML schema)
ms.assetid: 11fb3545-8974-4776-9a54-6b6e7739ae31
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5f11ed48d9dcf961228957cf15db3815c00d14d7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68204225"
---
# <a name="guidsymbol-element"></a>GuidSymbol 元素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

`GuidSymbol`元素包含表示菜单、 组或命令的 guid: id 对中的 GUID。 ID 来自`IDSymbol`中的元素`GuidSymbol`元素。 `GuidSymbol`元素具有`name`提供的 GUID，它包含在一个友好名称的属性`value`属性。  
  
## <a name="syntax"></a>语法  
  
```  
<GuidSymbol name="guidMyCommandSet" value="{xxxxxxxxxxxxx-xxxx-xxxx-xxxxxxxxxxxx}">  
  <IDSymbol>... </IDSymbol>  
  <IDSymbol>... </IDSymbol>  
</GuidSymbol>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|name|必需。 在 GUID 符号的名称。|  
|value|必需。 在 GUID 符号的 GUID。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[IDSymbol 元素](../extensibility/idsymbol-element.md)|包含表示菜单、 组或命令的 guid: id 对中的 ID。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[Symbols 元素](../extensibility/symbols-element.md)|组`GuidSymbol`.vsct 文件中的元素。|  
  
## <a name="remarks"></a>备注  
 通常情况下，在.vsct 文件包含三种`GuidSymbol`中的元素及其`Symbols`部分、 包本身的一个、 一个用于设置命令 （菜单、 组和包提供的命令的集合） 和一个用于提供的位图用于按钮和其他可视化组件的图标。 每个`IDSymbol`元素中的给定`GuidSymbol`元素必须具有一个唯一`value`。但是， `IDSymbol` ，只要它们具有不同的父，可以在包中存在具有相同的值的元素。  
  
## <a name="see-also"></a>请参阅  
 [Visual Studio 命令表格 (.Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
