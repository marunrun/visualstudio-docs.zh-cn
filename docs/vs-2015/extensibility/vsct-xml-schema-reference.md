---
title: VSCT XML 架构参考 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- Visual Studio command table configuration files (VSCT), XML schema
- VSCT XML schema elements
ms.assetid: 49e7efae-e713-4762-a824-96fdaf92cdc9
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e56de828d3b357762da98cde3b9591033c6b5d19
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63441480"
---
# <a name="vsct-xml-schema-reference"></a>VSCT XML 架构参考
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

提供一个命令表编译器架构元素，其中包含允许的子元素和属性为每个。  
  
 基于 XML 的命令表配置 (.vsct) 文件定义对集成的开发环境 (IDE) 的 VSPackage 提供的命令元素。 这些元素包括菜单项、 菜单、 工具栏和组合框。  
  
> [!NOTE]
> VSCT 编译器可以在.vsct 文件上运行预处理器。 这通常是因为C++预处理器，可以定义包含具有相同的语法中使用的宏和C++文件。 .Vsct 中提供了这样的示例文件**新的项目**为 VSPackage 项目创建向导。  
  
## <a name="optional-elements"></a>可选元素  
 某些 VSCT 元素是可选的。 如果`Parent`未指定参数，Group_Undefined:0将隐式。 如果`Icon`将暗示 guidOfficeIcon:msotcidNoIcon，未指定参数。 定义快捷键时，仿真，这是通常未使用，是可选的。  
  
 通过指定的位置中的位图条，可以在编译时嵌入位图项`href`参数。 位图条会在合并过程中复制而不是从该 DLL 的资源中提取。 当`href`提供参数，则`usedList`参数变为可选的并使用视为位图条带中的所有槽。  
  
 必须通过使用符号名称定义的所有 GUID 和 ID 值。 这些名称可能定义标头文件中或在 VSCT\<符号 > 部分。 符号名称必须是本地的包括通过\<Include > 元素，或所引用的\<Extern > 元素。 从在指定的标头文件中导入符号名称\<Extern > 元素，如果它遵循的简单的模式 #define 符号值。 值可能是另一个符号，只要以前定义该符号。 GUID 定义必须遵循任一 OLE 或C++格式。 ID 值可能是十进制数字或 0x，前面的十六进制数字，如以下代码行中所示：  
  
- {6D484634-E53D-4a2c-ADCB-55145C9362C8}  
  
- {0x6d484634、 0xe53d、 0x4a2c，{0xad、 0xcb，0x55、 0x14，0x5c、 0x93，0x62，0xc8}}  
  
  可以使用 XML 注释，但往返的图形用户界面 (GUI) 工具可能会放弃它们。 内容\<批注 > 元素都保证进行维护而不考虑格式。  
  
## <a name="schema-hierarchy"></a>架构层次结构  
 .Vsct 文件具有以下主要元素。  
  
 [CommandTable 元素](../extensibility/commandtable-element.md)  
  
 [Extern 元素](../extensibility/extern-element.md)  
  
 [ Include元素](../extensibility/include-element.md)  
  
 [Define 元素](../extensibility/define-element.md)  
  
 [Commands 元素](../extensibility/commands-element.md)  
  
 [CommandPlacements 元素](../extensibility/commandplacements-element.md)  
  
 [VisibilityConstraints 元素](../extensibility/visibilityconstraints-element.md)  
  
 [KeyBindings 元素](../extensibility/keybindings-element.md)  
  
 [UsedCommands 元素](../extensibility/usedcommands-element.md)  
  
 [Parent 元素](../extensibility/parent-element.md)  
  
 [Icon 元素](../extensibility/icon-element.md)  
  
 [Strings 元素](../extensibility/strings-element.md)  
  
 [ Command Flag元素](../extensibility/command-flag-element.md)  
  
 [Symbols 元素](../extensibility/symbols-element.md)  
  
 [条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)  
  
## <a name="see-also"></a>请参阅  
 [Vspackage 如何添加用户界面元素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)   
 [VSPackage 中的命令传送](../extensibility/internals/command-routing-in-vspackages.md)
