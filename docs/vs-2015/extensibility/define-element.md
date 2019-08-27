---
title: 定义元素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- VSCT XML schema elements, Define
- Define element (VSCT XML schema)
ms.assetid: 5aee74e3-de41-4dc6-9618-93e158af56dd
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8cc543a07176f307641c53a2ef3e132881821ce7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68162161"
---
# <a name="define-element"></a>Define 元素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

定义的符号名称和值对。 此符号可以评估的条件属性。 有关详细信息，请参阅[条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。 另请参阅[符号元素](../extensibility/symbols-element.md)。  
  
## <a name="syntax"></a>语法  
  
```  
<Define name="Mode" value="Standard" />  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|name|必需。 符号名称：<br /><br /> 名称 ="模式"|  
|值|必需。 符号的值：<br /><br /> value="Standard"|  
|条件|可选。 有关详细信息，请参阅[条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[CommandTable 元素](../extensibility/commandtable-element.md)|定义表示命令的 VSPackage 提供对集成的开发环境 (IDE) 的所有元素。 例如，菜单项、 菜单、 工具栏和组合框。|  
  
## <a name="example"></a>示例  
  
```  
<Define name="DEMO_UI"/>  
<Define name="MODE" value="Standard"/>  
```  
  
## <a name="see-also"></a>请参阅  
 [Visual Studio 命令表格 (.Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
