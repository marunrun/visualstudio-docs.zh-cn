---
title: 符号元素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- Symbols element (VSCT XML schema)
- VSCT XML schema elements, Symbols
ms.assetid: 1cda43d8-42a5-4b1b-a3c8-cf0401c3202f
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c8d28d225bd3a8d5c105bf54b9c63574002aed15
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68160464"
---
# <a name="symbols-element"></a>Symbols 元素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

定义其他 .VSCT 元素使用的 Guid 和 Id。 对于非托管代码，此信息通常来自 [Extern 元素](../extensibility/extern-element.md)指定的标头文件。 托管代码使用符号元素的子元素来定义此信息。  
  
 如果从现有的 cto 文件创建 .vsct 文件，则这些符号将作为符号元素的子元素生成。 有关详细信息，请参阅 [如何：创建。来自现有的 .vsct 文件。Cto 文件](../misc/how-to-create-a-dot-vsct-file-from-an-existing-dot-cto-file.md)。  
  
 符号元素不应与 [定义元素](../extensibility/define-element.md)混淆，后者定义要由预处理器使用的名称-值对。  
  
## <a name="syntax"></a>语法  
  
```  
<Symbols>  
  <GuidSymbol>... </GuidSymbol>  
  <GuidSymbol>... </GuidSymbol>  
</Symbols>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|说明|  
|---------------|-----------------|  
|无||  
  
### <a name="child-elements"></a>子元素  
  
|元素|说明|  
|-------------|-----------------|  
|GuidSymbol|定义 GUID 符号。 GuidSymbol 具有两个必需的属性： name 和 value。 Name 是符号的名称，值是以字符串形式的 GUID 的值。<br /><br /> 例如：\<GuidSymbol name="guidVsPackage1Pkg"   value="{c5f54698-101a-4846-84d3-dc748f9cd848}" />|  
|IDSymbol|定义一个符号。 IDSymbol 具有两个必需的属性： name 和 value。 Name 是符号名称，值为字符串形式的符号值。<br /><br /> 例如：\<IDSymbol name="MyMenuGroup" value="0x1020" />|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|说明|  
|-------------|-----------------|  
|[CommandTable 元素](../extensibility/commandtable-element.md)|.Vsct 文件的根元素。|  
  
## <a name="example"></a>示例  
  
```  
<Symbols>  
  <GuidSymbol name="guidVsPackage1Pkg" value="{c5f54698-101a-4846-84d3-dc748f9cd848}" />  
  <GuidSymbol name="guidVsPackage1CmdSet" value="{cb9dfd7f-2fcc-4a3e-aae8-f7fe30b1cfac}">  
    <IDSymbol name="MyMenuGroup" value="0x1020" />  
    <IDSymbol name="cmdidMyCommand" value="0x0100" />  
    <IDSymbol name="cmdidMyTool" value="0x0101" />  
  </GuidSymbol>  
</Symbols>  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Studio 命令表格 (.Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
