---
title: Visual Studio SDK)  (服务器 |Microsoft Docs
description: 本文介绍 Visual Studio 的调试器结构中的服务器的定义和角色。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- servers, debugging
- debugging [Debugging SDK], servers
ms.assetid: 62236d64-7956-448c-9ac3-5528f3edac1d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9eaccebf874fa5fc0e7aaf63823547742215a568
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2020
ms.locfileid: "96845292"
---
# <a name="servers-visual-studio-sdk"></a>服务器 (Visual Studio SDK)
在调试程序体系结构中， *服务器*：

- 是端口和端口供应商的容器，可将端口和端口供应商传达给会话调试管理器 (SDM) 和调试引擎。

- 可以按名称标识自身，并枚举其端口和端口供应商。

- 由 [IDebugCoreServer2](../../extensibility/debugger/reference/idebugcoreserver2.md) 接口表示，此接口仅由 visual studio 为运行) 的每个 visual studio 实例 (服务器的一个实例实现。

## <a name="see-also"></a>请参阅
- [端口](../../extensibility/debugger/ports.md)
- [端口供应商](../../extensibility/debugger/port-suppliers.md)
- [调试器概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugCoreServer2](../../extensibility/debugger/reference/idebugcoreserver2.md)
