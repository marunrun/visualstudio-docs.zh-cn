---
title: 枚举器 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, enumerators
ms.assetid: a60030c5-e1d1-47e1-84bb-cbfe838ab479
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ee48d064612e5519d5ad7e5eaf04de6c5a697837
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711859"
---
# <a name="enumerators"></a>枚举器
本节列出了源代码管理插件 API 中的枚举器数据类型，源代码管理插件必须了解这些数据类型。

## <a name="in-this-section"></a>在本节中
- [命令代码](../extensibility/command-code-enumerator.md)枚举[SccGet命令选项](../extensibility/sccgetcommandoptions-function.md)和[Scc 填充列表](../extensibility/sccpopulatelist-function.md)函数的选项。

- [消息](../extensibility/message-enumerator.md)枚举用于打印回调[、LPTEXTOUTPROC](../extensibility/lptextoutproc.md)的标志。

- [文件状态代码](../extensibility/file-status-code-enumerator.md)包含指定源控制下文件状态的命名常量值。

- [目录状态代码](../extensibility/directory-status-code-enumerator.md)包含指定源控制下的目录状态的命名常量值。

## <a name="related-sections"></a>相关章节
- [创建源代码管理插件](../extensibility/internals/creating-a-source-control-plug-in.md)定义源代码管理插件 SDK 并描述包含的资源。

- [SccGet命令选项](../extensibility/sccgetcommandoptions-function.md)提示用户为给定命令提供高级选项。

- [Scc填充列表](../extensibility/sccpopulatelist-function.md)检查文件列表的当前状态。 此外，当文件与`pfnPopulate`的条件`nCommand`不匹配时，使用 函数通知调用方。

- [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)描述[SccOpenProject](../extensibility/sccopenproject-function.md)用于通过 IDE 显示来自源代码管理插件的消息的回调功能。

- [源代码管理插件](../extensibility/source-control-plug-ins.md)提供源代码管理插件 API 中所有元素的完整列表。
