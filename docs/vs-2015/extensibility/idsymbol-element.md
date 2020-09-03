---
title: IDSymbol 元素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDSymbol element (VSCT XML schema)
- VSCT XML schema elements, IDSymbol
ms.assetid: 760cfd20-3c06-422c-9103-98bfa1f387f8
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7db4e686b5e105b0ea0aa80783137093679d4cad
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68203969"
---
# <a name="idsymbol-element"></a>IDSymbol 元素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

`IDSymbol`元素包含表示菜单、组或命令的 GUID： id 对的 id。 GUID 来自父 `GuidSymbol` 元素。 `IDSymbol`元素具有一个 `name` 属性，该属性提供 ID 的友好名称，该名称包含在属性中 `value` 。  
  
## <a name="syntax"></a>语法  
  
```  
<IDSymbol name=ElementName value="0x0010" />  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|说明|  
|---------------|-----------------|  
|name|必需。 ID 符号的名称。|  
|值|必需。 ID 符号的数字 ID 值。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|说明|  
|-------------|-----------------|  
|[GuidSymbol 元素](../extensibility/guidsymbol-element.md)|包含表示菜单、组或命令的 GUID： ID 对的 GUID。 对 `IDSymbol` 元素进行分组。|  
  
## <a name="remarks"></a>备注  
 `IDSymbol`给定元素中的每个元素 `GuidSymbol` 必须具有唯一的 `value` 。 但是， `IDSymbol` 具有相同值的元素可以存在于包中，只要它们具有不同的父元素。  
  
## <a name="see-also"></a>另请参阅  
 [Visual Studio 命令表格 (.Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
