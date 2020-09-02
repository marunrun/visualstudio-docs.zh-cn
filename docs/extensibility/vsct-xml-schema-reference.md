---
title: .VSCT XML 架构参考 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio command table configuration files (VSCT), XML schema
- VSCT XML schema elements
ms.assetid: 49e7efae-e713-4762-a824-96fdaf92cdc9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 923a0c4b64fcae3a409a2298d6d481f6e1bb14db
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80697906"
---
# <a name="vsct-xml-schema-reference"></a>.VSCT XML 架构引用
提供一个表，其中包含命令表编译器架构元素，每个元素都允许使用子元素和属性。

 一个基于 XML 的命令表配置 (. .vsct) file 定义 VSPackage 向集成开发环境 (IDE) 提供的命令元素。 这些元素包括菜单项、菜单、工具栏和组合框。

> [!NOTE]
> .VSCT 编译器可以对 .vsct 文件运行预处理器。 由于这通常是 c + + 预处理器，因此你可以定义具有与 c + + 文件中所用语法相同的语法的包含和宏。 **新项目**向导为 VSPackage 项目创建的 .vsct 文件中提供了这种情况的示例。

## <a name="optional-elements"></a>可选元素
 某些 .VSCT 元素是可选的。 如果 `Parent` 未指定参数，则 Group_Undefined：0将隐式。 如果 `Icon` 未指定参数，则将隐式 guidOfficeIcon： msotcidNoIcon。 定义快捷键后，通常不使用的仿真是可选的。

 在编译时，可以通过在参数中指定位图条的位置来嵌入位图项 `href` 。 在合并过程中将复制位图条，而不是从 DLL 的资源中提取。 如果 `href` 提供了参数，则 `usedList` 参数将变为可选，并且会将位图条中的所有槽视为已使用。

 所有 GUID 和 ID 值都必须通过使用符号名称来定义。 可以在头文件中或在 .VSCT 节中定义这些名称 \<Symbols> 。 符号名称必须是本地的、包含在 \<Include> 元素中或由 \<Extern> 元素引用。 如果符号名称 \<Extern> 遵循 #define 符号值的简单模式，则从元素中指定的标头文件中导入。 此值可以是另一个符号，只要该符号以前已定义。 GUID 定义必须遵循 OLE 或 c + + 格式。 ID 值可以是十进制数字，也可以是以0x 开头的十六进制数字，如以下行所示：

- {6D484634-E53D-4a2c-ADCB-55145C9362C8}

- {0x6d484634，0xe53d，0x4a2c，{0xad，0xcb，0x55，0x14，0x5c，0x93，0x62，0xc8}}

  可以使用 XML 注释，但 (GUI) 工具可能会丢弃这些注释。 \<Annotation>无论采用哪种格式，都保证元素的内容得以维护。

## <a name="schema-hierarchy"></a>架构层次结构
 .Vsct 文件包含以下主要元素。

- [CommandTable 元素](../extensibility/commandtable-element.md)

- [Extern 元素](../extensibility/extern-element.md)

- [Include 元素](../extensibility/include-element.md)

- [Define 元素](../extensibility/define-element.md)

- [命令元素](../extensibility/commands-element.md)

- [CommandPlacements 元素](../extensibility/commandplacements-element.md)

- [VisibilityConstraints 元素](../extensibility/visibilityconstraints-element.md)

- [键绑定元素](../extensibility/keybindings-element.md)

- [UsedCommands 元素](../extensibility/usedcommands-element.md)

- [父元素](../extensibility/parent-element.md)

- [Icon 元素](../extensibility/icon-element.md)

- [Strings 元素](../extensibility/strings-element.md)

- [命令标志元素](../extensibility/command-flag-element.md)

- [符号元素](../extensibility/symbols-element.md)

- [条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)

## <a name="see-also"></a>另请参阅
- [Vspackage 如何添加用户界面元素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [Vspackage 中的命令传送](../extensibility/internals/command-routing-in-vspackages.md)
