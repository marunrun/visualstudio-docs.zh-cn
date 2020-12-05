---
title: 模块 |Microsoft Docs
description: 本文介绍 Visual Studio 的调试器结构中的模块的定义和角色。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- modules
- debugging [Debugging SDK], modules
ms.assetid: c4cf2809-dbdb-4e75-9273-b3d3d77b67d0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 57202231c1bbfc7712d322b8cc7a30e3f64c87af
ms.sourcegitcommit: 42981ace63c0f2b087de5703ca76b8dcdd93a719
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2020
ms.locfileid: "96606640"
---
# <a name="modules"></a>模块
就调试器体系结构而言， *模块* 如下：

- 是一个物理代码容器，如可执行文件或 DLL。

- 可以重新加载其符号并对其进行描述。 模块说明显示在 IDE 的 "模块" 窗口中。

- 由调试引擎创建的 [IDebugModule2](../../extensibility/debugger/reference/idebugmodule2.md) 接口表示，用于说明模块。

## <a name="see-also"></a>请参阅
- [调试器概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugModule2](../../extensibility/debugger/reference/idebugmodule2.md)
