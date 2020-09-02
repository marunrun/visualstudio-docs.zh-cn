---
title: String 元素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- Strings element (VSCT XML schema)
- VSCT XML schema elements, Strings
ms.assetid: 23a42074-a689-481d-824f-b43aa448f266
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0eae2fd7490269d713beb9950163071dd3ba32f5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68160567"
---
# <a name="strings-element"></a>Strings 元素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

String 元素必须包含至少一个 **ButtonText** 子元素。 所有其他子元素都是可选的。 无效的 XML 字符（如 "&" 和 "<"）必须编码为实体 ( " &amp; " 和 " &lt;) " 等。  
  
 文本字符串中的 "and" 符指定了命令的键盘快捷方式。  
  
## <a name="syntax"></a>语法  
  
```  
<Strings>  
  <ButtonText>... </ButtonText>  
  <CommandName>... </CommandName>  
</Strings>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|说明|  
|---------------|-----------------|  
|语言|可选。 Language = "."。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|说明|  
|-------------|-----------------|  
|ButtonText|在命令定义中，此字段和五个以下文本字段可用于指定在各种菜单中显示的文本。 默认情况下，该 `ButtonText` 字段显示在菜单控制器中。 `ButtonText`如果其他文本字段为空，则字段也成为默认字段。 `ButtonText`即使指定了其他文本字段，字段也不能为空。|  
|ToolTipText|`ToolTipText`字段指定在菜单项的工具提示中显示的文本。<br /><br /> 如果该 `ToolTipText` 字段为空，则 `ButtonText` 使用该字段。|  
|MenuText|`MenuText`字段指定了在主菜单、工具栏、快捷菜单或子菜单中显示的命令所显示的文本。 如果该 `MenuText` 字段为空，则集成开发环境 (IDE) 使用 `ButtonText` 字段。 该 `MenuText` 字段还可用于本地化。<br /><br /> 对于快捷菜单，该 `MenuText` 字段是显示在快捷菜单工具栏中的名称，可用于在 IDE 中自定义快捷菜单。 因此，请具体了解快捷菜单的命名方式;例如，使用 "小组件包快捷菜单" 而不是 "快捷方式"。<br /><br /> 如果 `MenuText` 未指定字段，则 `ButtonText` 使用字段。|  
|CommandName|`CommandName`字段指定 "**自定义**" 对话框的 "**命令**" 选项卡中的 "键盘" 类别中显示的文本， (可通过单击 "**工具**" 菜单上的 "**自定义**") 。|  
|CanonicalName|英语 `CanonicalName` 字段指定可以在 " **命令** " 窗口中输入的命令的名称以执行菜单项。 IDE 将去除不是字母、数字、下划线或嵌入句点的任何字符。 然后，将此文本连接到 `ButtonText` 字段以定义该命令。 例如，"**文件**" 菜单上的 "**新建项目**" 将成为 NewProject 命令。<br /><br /> 如果 `CanonicalName` 未指定英语字段，IDE 将使用 `ButtonText` 字段，并去除除字母、数字、下划线和嵌入句点以外的所有字符。 例如，按钮文本 "&定义命令 ..."变为 DefineCommands，其中，与号、空格和省略号一起被移除。<br /><br /> 如果 `TextChanges` 指定了标志，并且更改了命令的文本，则 **命令** 窗口识别的相应命令不会更改; 它仍是原始 `ButtonText` 字段或英语字段的规范形式 `CanonicalName` 。|  
|LocCanonicalName|该 `LocCanonicalName` 字段的行为与英语字段的行为相同， `CanonicalName` 但会启用要指定的本地化命令文本。 这两个规范字段都可以指定。 由于 IDE 仅分析在 " **命令** " 窗口中输入的文本，并将其与命令相关联，因此英语文本和非英语文本都可以与同一命令相关联。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|说明|  
|-------------|-----------------|  
|[Button 元素](../extensibility/button-element.md)|定义用户可与之交互的元素。|  
|[Menu 元素](../extensibility/menu-element.md)|定义单个菜单项。|  
|[Combo 元素](../extensibility/combo-element.md)|定义在组合框中显示的命令。|  
  
## <a name="see-also"></a>另请参阅  
 [Visual Studio 命令表格 (.Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
