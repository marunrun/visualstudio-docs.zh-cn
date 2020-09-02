---
title: IDE 实现的回调函数 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80739890"
---
# <a name="callback-functions-implemented-by-the-ide"></a>IDE 实现的回调函数
为了与集成开发环境集成 (IDE) 尽可能无缝地进行集成，并提供统一的最终用户体验，则源代码管理插件可以使用 IDE 实现的回调函数。 在源代码管理操作期间，该插件可以在适当的时间调用这些函数，以将信息传递到 IDE;然后，IDE 可以在其本机 UI 中将此信息显示为嵌入元素。 在此方案中，用户的工作效率较低，但该插件使用自己的 UI。

 所需的标头文件是 *scc. h*。 默认位置为*\Program Files\VSIP 8.0 \ EnvSDK\common\inc \\ *。 它还包含在*\Program Files\VSIP 8.0 \ MSSCCI \\ *源代码管理插件示例的 VSIP 文件夹中。

## <a name="in-this-section"></a>本节内容
- [LPTEXTOUTPROC](../extensibility/lptextoutproc.md) 描述 [SccOpenProject](../extensibility/sccopenproject-function.md) 用于通过 IDE 显示源代码管理插件消息的回调函数。

- [POPLISTFUNC](../extensibility/poplistfunc.md) 描述当 IDE 无法完全访问仅适用于源代码管理插件的信息（如版本控制下的文件的完整列表）时， [SccPopulateList](../extensibility/sccpopulatelist-function.md) 使用的回调函数。

- [QUERYCHANGESFUNC](../extensibility/querychangesfunc.md) 描述 [SccQueryChanges](../extensibility/sccquerychanges-function.md) 操作使用的回调函数。

- [POPDIRLISTFUNC](../extensibility/popdirlistfunc.md) 描述 [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md) 操作使用的回调函数。

- [OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md) 描述通过调用 [SccSetOption](../extensibility/sccsetoption-function.md) 设置的回调函数，该函数使源代码管理插件能够将名称更改传递回 IDE。

## <a name="related-sections"></a>相关章节
- [SccOpenProject](../extensibility/sccopenproject-function.md) 打开项目。

- [SccPopulateList](../extensibility/sccpopulatelist-function.md) 检查文件列表的当前状态。 此外， `pfnPopulate` 如果文件与的条件不匹配，则使用函数通知调用方 `nCommand` 。

- [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md) 检查项目或受源代码管理的项目中的目录和文件的列表。 找到的每个目录和文件名都将传递到回调函数。

- [SccQueryChanges](../extensibility/sccquerychanges-function.md) 检查对文件列表进行的名称更改。 每个文件名都将与其更改状态一起传递给回调函数。

- [SccSetOption](../extensibility/sccsetoption-function.md) 设置各种选项。 每个选项都以开头 `SCC_OPT_xxx` ，并且具有其自己定义的值集。

- [源代码管理插件](../extensibility/source-control-plug-ins.md) 介绍源代码管理插件 SDK 的 "引用" 部分的内容。
