---
title: Icon 元素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- VSCT XML schema elements, Icon
- Icon element (VSCT XML schema)
ms.assetid: 73c58fe3-d53c-4f4e-b025-29567c6cbb7c
caps.latest.revision: 6
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ca5ced87596b5e40ae70e3faa06e58493da3d8ab
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68203995"
---
# <a name="icon-element"></a>Icon 元素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

图标标记的 guid 属性是定义的位图的 guid。  Id 属性在位图带区中选择槽。 此元素为可选元素。  如果省略此元素，则将隐式 **guidOfficeIcon： msotcidNoIcon** 的值。  
  
## <a name="syntax"></a>语法  
  
```  
<Icon guid="guidImages" id="bmpPic1" />  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|说明|  
|---------------|-----------------|  
|guid|必需。 定义的位图的 guid。|  
|id|必需。 选择位图条中的槽。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|说明|  
|-------------|-----------------|  
|无。|无。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|说明|  
|-------------|-----------------|  
|[Buttons 元素](../extensibility/buttons-element.md)||  
  
## <a name="see-also"></a>另请参阅  
 [Visual Studio 命令表格 (.Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
