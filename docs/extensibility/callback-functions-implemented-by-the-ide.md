---
title: 通过 IDE 实现的回调函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, callback functions
- callback functions, source control plug-ins
ms.assetid: 4a8833f0-6ac0-4ea7-9400-8275aa991468
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dff6ee0a81472ea556aaca478a2ff33db93fe871
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66321172"
---
# <a name="callback-functions-implemented-by-the-ide"></a>通过 IDE 实现的回调函数
为了使与集成为尽可能，并提供了统一的最终用户体验，无缝集成的开发环境 (IDE) 的源代码管理插件可以使用通过 IDE 实现的回调函数。 该插件可调用这些函数在将信息传递到 IDE; 源代码管理操作期间的适当时间IDE 可以显示此信息作为其本机用户界面中的嵌入元素。 用户必须在此方案中比如果插件，则使用自己的 UI 不太零碎的体验。

 必需的标头文件是*scc.h*。 默认位置是 *\Program Files\VSIP 8.0\EnvSDK\common\inc\\* 。 它也是已在源控件插件示例的 VSIP 文件夹 *\Program Files\VSIP 8.0\MSSCCI\\* 。

## <a name="in-this-section"></a>本节内容
- [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)描述使用的回调函数[SccOpenProject](../extensibility/sccopenproject-function.md)以显示从源代码管理插件通过 IDE 的消息。

- [POPLISTFUNC](../extensibility/poplistfunc.md)描述使用的回调函数[SccPopulateList](../extensibility/sccpopulatelist-function.md) IDE 不具有完全访问仅向源代码管理插件，例如，完整的列表提供的信息版本控制下的文件。

- [QUERYCHANGESFUNC](../extensibility/querychangesfunc.md)描述使用的回调函数[SccQueryChanges](../extensibility/sccquerychanges-function.md)操作。

- [POPDIRLISTFUNC](../extensibility/popdirlistfunc.md)描述使用的回调函数[SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md)操作。

- [OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md)介绍了通过调用设置的回调函数[SccSetOption](../extensibility/sccsetoption-function.md)启用源代码管理插件通信名称更改回 IDE。

## <a name="related-sections"></a>相关章节
- [SccOpenProject](../extensibility/sccopenproject-function.md)打开一个项目。

- [SccPopulateList](../extensibility/sccpopulatelist-function.md)检查以了解其当前状态的文件的列表。 此外，使用`pfnPopulate`函数，以通知调用方，当文件不匹配的条件时`nCommand`。

- [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md)检查中一个项目或项目源代码管理下的目录和文件的列表。 找到每个目录和文件名称传递给回调函数。

- [SccQueryChanges](../extensibility/sccquerychanges-function.md)检查所做的文件列表的名称更改。 每个文件名传递给回调函数以及将其更改状态。

- [SccSetOption](../extensibility/sccsetoption-function.md)设置各种选项。 每个选项开始`SCC_OPT_xxx`并具有其自己定义的值集。

- [源代码管理插件](../extensibility/source-control-plug-ins.md)描述源控件插件 SDK 的参考部分的内容。