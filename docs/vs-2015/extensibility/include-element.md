---
title: 包含元素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- Include
helpviewer_keywords:
- Include element (VSCT XML schema)
- VSCT XML schema elements, Include
ms.assetid: c923dfe6-084a-4105-aec1-f0a3f8399c54
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1bdc56c9d0b488bdbe24a8534ab516cc0fc831df
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68203933"
---
# <a name="include-element"></a>Include 元素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Include 元素指定的文件，可以找到对提供包括插入到当前文件的路径。  所有符号和定义的类型将都成为已编译的结果的一部分。  
  
## <a name="syntax"></a>语法  
  
```csharp  
<Include href="stdidcmd.h" />  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|href|必需。 标头文件的路径：<br /><br /> href="stdidcmd.h"|  
|条件|可选。 请参阅[条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|无。|无。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[CommandTable 元素](../extensibility/commandtable-element.md)|定义表示命令的元素的所有 — 也就是说，菜单项、 菜单、 工具栏和组合框 — VSPackage 提供到 IDE。|  
  
## <a name="example"></a>示例  
  
```  
<Include href="PackagePlacements.vsct"/>  
```  
  
## <a name="see-also"></a>请参阅  
 [Visual Studio 命令表格 (.Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
