---
title: 使程序被调试 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], enabling for programs
ms.assetid: 61d24820-0cd9-48b6-8674-6813f7493237
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 17c6218cd0b25c0cf0134351fd5efd7490b6a1f3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738891"
---
# <a name="enable-a-program-to-be-debugged"></a>启用对程序进行调试
在调试引擎 （DE） 可以调试程序之前，必须首先启动 DE 或将其附加到现有程序。

## <a name="in-this-section"></a>在本节中
 [获取端口](../../extensibility/debugger/getting-a-port.md)讨论如何获取端口作为启用程序调试的第一步。

 [注册程序](../../extensibility/debugger/registering-the-program.md)解释启用程序调试的下一步：将其注册到端口。 注册后，可以通过附加或及时 （JIT） 调试过程对程序进行调试。

 [附加到程序](../../extensibility/debugger/attaching-to-the-program.md)解释下一步：将调试器附加到程序。

 [基于启动的附加](../../extensibility/debugger/launch-based-attachment.md)描述程序基于启动的附件，SDM 在启动时自动进行该附件。

 [发送所需事件](../../extensibility/debugger/sending-the-required-events.md)在创建调试引擎 （DE） 并将其附加到程序时，执行所需的事件。

## <a name="related-sections"></a>相关章节
 [创建自定义调试引擎](../../extensibility/debugger/creating-a-custom-debug-engine.md)定义调试引擎 （DE），并描述通过 DE 接口实现的服务，以及它们如何导致调试器在不同操作模式之间转换。
