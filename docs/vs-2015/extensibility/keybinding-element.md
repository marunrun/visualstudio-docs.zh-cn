---
title: KeyBinding 元素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- VSCT XML schema elements, KeyBindings
- KeyBinding element (VSCT XML schema)
ms.assetid: e55a1098-15df-42a9-9f87-e3a99cf437dd
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 75d96098e8444aac9a4fc6f895099435b54f640b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68180330"
---
# <a name="keybinding-element"></a>KeyBinding 元素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

键绑定元素指定的命令的键盘快捷方式。  
  
 命令可以具有与之关联的单个和双键绑定。 单个键绑定的一个示例是为 CTRL + S**保存**命令。 双键绑定需要两个连续的键组合来触发命令。 双键绑定的一个示例是 CTRL + K、 CTRL + K 设置书签。  
  
## <a name="syntax"></a>语法  
  
```  
<Keybinding guid="MyGuid" id="MyId" Editor="MyEditor" key1="B" key2="x" mod1="Control" mod2="Alt" />  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|guid|必需。|  
|id|必需。|  
|编辑器|必需。 编辑器 GUID 指示为其此键盘快捷方式将处于活动状态的编辑上下文。 全局绑定作用域值为"guidVSStd97"。|  
|key1|必需。 有效值包括所有键入是字母数字和也两位数字的十六进制值 0x 和 VK_constants 前面有。|  
|mod1|可选。 CTRL、 ALT 和 SHIFT 空格分隔的任意组合。|  
|key2|可选。 有效值包括所有键入是字母数字和也两位数字的十六进制值 0x 和 VK_constants 前面有。|  
|mod2|可选。 CTRL、 ALT 和 SHIFT 空格分隔的任意组合。|  
|仿真程序|可选。|  
|条件|可选。 请参阅[条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|父级||  
|批注||  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[KeyBindings 元素](../extensibility/keybindings-element.md)|键绑定元素进行分组和其他键绑定分组。|  
  
## <a name="example"></a>示例  
  
```  
<KeyBindings>  
  <KeyBinding guid="guidWidgetPackage" id="cmdidUpdateWidget"   
    editor="guidWidgetEditor" key1="VK_F5"/>  
  <KeyBinding guid="guidWidgetPackage" id="cmdidRunWidget"   
    editor="guidWidgetEditor" key1="VK_F5" mod1="Control"/>  
</KeyBindings>  
```  
  
## <a name="see-also"></a>请参阅  
 [KeyBindings 元素](../extensibility/keybindings-element.md)   
 [Visual Studio 命令表格 (.Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
