---
title: Extern 元素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- Extern
helpviewer_keywords:
- VSCT XML schema elements, Extern
- Extern element (VSCT XML schema)
ms.assetid: db6c3ddd-a1ba-450a-897a-bb568a5377fc
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 17477b7eb60aa332f6910019e28f4c53aa31ebf1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204400"
---
# <a name="extern-element"></a>Extern 元素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Extern 元素在编译时引用 () 文件与 .vsct 文件合并的任何外部标头。 要合并的文件必须位于 .VSCT 编译器提供的包含路径上，或由 [Include 元素](../extensibility/include-element.md)引用。 这些文件可以是其他 .vsct 文件或 c + + 头文件。  
  
 标头文件中的定义的格式必须为 "#define [符号] [值]"。值可以是其他符号（如果以前已定义）。 定义可以在命令项的条件语句中使用。 不实际使用的任何符号将被丢弃。  
  
 CommandTable 元素  
Extern 元素  
  
## <a name="syntax"></a>语法  
  
```  
<Extern href="stdidcmd.h" />  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|说明|  
|---------------|-----------------|  
|href|必需。 标头文件的路径：<br /><br /> href = "stdidcmd"|  
|条件|可选。 请参阅 [条件特性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|  
|语言|可选。 [\<Strings>](../extensibility/strings-element.md)命令表中所有元素的默认语言：<br /><br /> language = "en-us"|  
  
### <a name="child-elements"></a>子元素  
  
|元素|说明|  
|-------------|-----------------|  
|无。|无。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|说明|  
|-------------|-----------------|  
|[CommandTable 元素](../extensibility/commandtable-element.md)|定义所有元素，这些元素表示 VSPackage 提供给 IDE 的命令（即菜单项、菜单、工具栏和组合框）。|  
  
## <a name="example"></a>示例  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<CommandTable xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-  
  18/CommandTable" xmlns:xs="http://www.w3.org/2001/XMLSchema">  
    <Extern href="C:\VSCore\vscommon\inc\vsshlids.h"/>  
    …  
  <Commands package="guidMyPackage">  
</CommandTable>  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Studio 命令表 (。.Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)   
 [Vspackage 如何添加用户界面元素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)   
 [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)
