---
title: 跨多个项目连接应用设置 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, application of settings
ms.assetid: 2116d3d0-c46c-4d0a-b482-08a178584f46
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bcaed0f7f2380dd36bcbffd776839025fe9efa16
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710063"
---
# <a name="application-of-settings-across-multiple-project-connections"></a>跨多个项目连接应用设置
使用源代码管理插件 API 版本 1.2 构建的源代码管理插件可以使用批处理操作跨多个项目或多个连接上下文执行相同的源代码管理操作。 批处理可用于从用户体验中消除冗余的每个项目对话框。

 如果用户选择多个项属于使用源代码管理插件 API 版本 1.1 构建的源代码管理插件中的多个连接，并检查它们，则用户会反复看到同一对话框。 即使用户单击对话框中的"**适用于所有"** 复选框，也会发生此情况，因为 IDE 会为每个连接上下文重置其状态。

## <a name="new-capability-flag"></a>新功能标志
 该`SccBeginBatch`函数设置`SCC_CAP_BATCH`标志以指示批处理操作正在进行。

## <a name="new-functions"></a>新函数
以下新功能支持批处理操作：

- [SccBeginBatch](../../extensibility/sccbeginbatch-function.md)

- [SccEndBatch](../../extensibility/sccendbatch-function.md)

该`SCCBeginBatch`函数启动一组源代码管理操作。 函数`SccEndBatch`关闭组。 组可能无法嵌套。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 版本 1.2 中的新增功能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
