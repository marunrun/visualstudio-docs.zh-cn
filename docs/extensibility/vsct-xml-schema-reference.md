---
title: VSCT XML 架构参考 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697906"
---
# <a name="vsct-xml-schema-reference"></a>VSCT XML 架构引用
提供命令表编译器架构元素的表，每个元素都允许子元素和属性。

 基于 XML 的命令表配置 （.vsct） 文件定义 VSPackage 向集成开发环境 （IDE） 提供的命令元素。 这些元素包括菜单项、菜单、工具栏和组合框。

> [!NOTE]
> VSCT 编译器可以在 .vsct 文件上运行预处理器。 由于这通常是C++预处理器，因此可以定义具有与C++文件相同的语法的包含和宏。 新项目向导为 VSPackage**项目**创建的 .vsct 文件中提供了这方面的示例。

## <a name="optional-elements"></a>可选元素
 某些 VSCT 元素是可选的。 如果未指定`Parent`参数，则Group_Undefined：0将被暗示。 如果未指定`Icon`参数，则暗示为 guidOfficeIcon：msotcidNoIcon。 定义快捷键时，通常未使用的仿真是可选的。

 通过在`href`参数中指定位图条的位置，可以在编译时嵌入位图项。 位图条条在合并期间复制，而不是从 DLL 的资源中提取。 提供`href`参数时，参数`usedList`变为可选，并且考虑使用位图条中的所有插槽。

 所有 GUID 和 ID 值都必须使用符号名称来定义。 这些名称可以在标题文件中或在 VSCT\<符号>部分中定义。 符号名称必须是本地的，通过\<"包括>元素包含"，或者由\<Extern> 元素引用。 符号名称从\<Extern> 元素中指定的标头文件中导入，如果它遵循#define SYMBOL VALUE 的简单模式。 只要该符号以前定义，该值可能是另一个符号。 GUID 定义必须遵循 OLE 或C++格式。 ID 值可以是十进制数字或十六进制数字，前面是 0x，如以下行所示：

- [6D484634-E53D-4a2c-ADCB-55145C9362C8]

- { 0x6d484634， 0xe53d， 0x4a2c， { 0xad， 0xcb， 0x55， 0x14， 0x5c， 0x93， 0x62， 0xc8 |

  可以使用 XML 注释，但往返图形用户界面 （GUI） 工具可能会放弃它们。 \<无论格式如何，注释>元素的内容都保证得到维护。

## <a name="schema-hierarchy"></a>架构层次结构
 .vsct 文件具有以下主要元素。

- [命令表元素](../extensibility/commandtable-element.md)

- [外部元素](../extensibility/extern-element.md)

- [包括元素](../extensibility/include-element.md)

- [定义元素](../extensibility/define-element.md)

- [命令元素](../extensibility/commands-element.md)

- [命令放置元素](../extensibility/commandplacements-element.md)

- [可见性约束元素](../extensibility/visibilityconstraints-element.md)

- [键绑定元素](../extensibility/keybindings-element.md)

- [已用命令元素](../extensibility/usedcommands-element.md)

- [父元素](../extensibility/parent-element.md)

- [图标元素](../extensibility/icon-element.md)

- [字符串元素](../extensibility/strings-element.md)

- [命令标志元素](../extensibility/command-flag-element.md)

- [符号元素](../extensibility/symbols-element.md)

- [条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)

## <a name="see-also"></a>请参阅
- [VS包如何添加用户界面元素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [VS 包中的命令路由](../extensibility/internals/command-routing-in-vspackages.md)
