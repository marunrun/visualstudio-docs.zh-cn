---
title: 跨多个项目连接设置的应用程序 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, application of settings
ms.assetid: 2116d3d0-c46c-4d0a-b482-08a178584f46
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 480ccaac58e67a959454e9d4afa9aa57e817c693
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66315844"
---
# <a name="application-of-settings-across-multiple-project-connections"></a>跨多个项目连接设置的应用程序
源代码管理插件使用源控制插件 API 版本 1.2，生成可用于批处理操作执行相同的源代码管理操作跨多个项目或多个连接上下文。 若要消除冗余，每个项目对话框从用户体验，可以使用批处理。

 如果用户选择多个项属于使用源控制插件 API 版本 1.1 （例如，在不同的文件共享计算机上两个 web 项目） 生成的源代码管理插件中的多个连接，并检查它们，用户将看到相同对话框中重复。 即使用户单击也会出现这种情况下**应用到所有**中的复选框的对话框中，因为 IDE 将重置其状态，以便每个连接上下文。

## <a name="new-capability-flag"></a>新的功能标志
 `SccBeginBatch`函数集`SCC_CAP_BATCH`标志，用于指示批处理操作正在进行。

## <a name="new-functions"></a>新的函数
以下新函数支持批处理操作：

- [SccBeginBatch](../../extensibility/sccbeginbatch-function.md)

- [SccEndBatch](../../extensibility/sccendbatch-function.md)

`SCCBeginBatch`函数启动的源代码管理操作组。 `SccEndBatch`函数将关闭的组。 不能嵌套组。

## <a name="see-also"></a>请参阅
- [什么是源控制插件 API 版本 1.2 中的新增功能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)