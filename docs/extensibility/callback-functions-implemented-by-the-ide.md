---
title: IDE 实现的回调功能 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, callback functions
- callback functions, source control plug-ins
ms.assetid: 4a8833f0-6ac0-4ea7-9400-8275aa991468
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 666486f5b800707a4467a129abeed7a13306f10a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739890"
---
# <a name="callback-functions-implemented-by-the-ide"></a>IDE 实现的回调功能
为了使与集成开发环境 （IDE） 的集成尽可能无缝，并提供统一的最终用户体验，源代码管理插件可以使用 IDE 实现的回调功能。 插件可以在源代码管理操作期间的适当时间调用这些函数，以将信息传递给 IDE;然后，IDE 可以将其本地 UI 中的嵌入元素显示此信息。 与插件使用其自己的 UI 相比，用户在此方案中具有较少碎片化的体验。

 所需的头文件是*scc.h*。 默认位置是 *[程序文件]VSIP 8.0\EnvSDK_common_inc\\*。 它还在 VSIP 文件夹中，该文件夹在 *[程序文件]VSIP 8.0_MSSCCI\\*处具有源代码管理插件示例。

## <a name="in-this-section"></a>在本节中
- [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)描述[SccOpenProject](../extensibility/sccopenproject-function.md)用于通过 IDE 显示来自源代码管理插件的消息的回调功能。

- [POPLISTFUNC](../extensibility/poplistfunc.md)描述[SccPopulateList](../extensibility/sccpopulatelist-function.md)在 IDE 无法完全访问仅对源代码管理插件可用的信息（如版本控制下的文件的完整列表）时使用的回调功能。

- [查询更改](../extensibility/querychangesfunc.md)描述[SccQuery 更改](../extensibility/sccquerychanges-function.md)操作使用的回调功能。

- [波普迪利斯芬奇](../extensibility/popdirlistfunc.md)描述[SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md)操作使用的回调函数。

- [OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md)描述对[SccSetOption](../extensibility/sccsetoption-function.md)的调用设置的回调功能，该调用使源代码管理插件能够将名称更改传回 IDE。

## <a name="related-sections"></a>相关章节
- [SccOpen项目](../extensibility/sccopenproject-function.md)打开项目。

- [Scc填充列表](../extensibility/sccpopulatelist-function.md)检查文件列表的当前状态。 此外，当文件与`pfnPopulate`的条件`nCommand`不匹配时，使用 函数通知调用方。

- [SccpopulateDirlist](../extensibility/sccpopulatedirlist-function.md)检查受源代码管理的项目或项目中的目录和文件的列表。 找到的每个目录和文件名都传递给回调函数。

- [SccQuery 更改](../extensibility/sccquerychanges-function.md)检查对文件列表所做的名称更改。 每个文件名都传递给回调函数及其更改状态。

- [SccSetOption](../extensibility/sccsetoption-function.md)设置各种选项。 每个选项都从`SCC_OPT_xxx`并有自己的定义值集开始。

- [源代码管理插件](../extensibility/source-control-plug-ins.md)描述源代码管理插件 SDK 的参考部分的内容。
