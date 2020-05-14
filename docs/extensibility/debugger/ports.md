---
title: 端口 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- ports
- debugging [Debugging SDK], ports
ms.assetid: 1d7f3aa7-7eff-4cab-bc53-0a566b1a9363
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7b42e7fa97c12afa07923e99d8b084840ee7ccad
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738292"
---
# <a name="ports"></a>端口
在调试器体系结构中，*端口*：

- 是服务器上运行的一组进程的容器。 例如，端口可能通过串行电缆或网络非 DCOM 计算机表示与基于 Windows CE 的设备的连接。 一个称为本地端口的特殊端口包含在本地计算机上运行的所有进程。

- 可以按名称或标识符标识自身。

- 可以枚举在端口上运行的所有进程，并启动和终止这些进程。

- 由[IDebugPort2](../../extensibility/debugger/reference/idebugport2.md)接口表示，该接口通过将[IDebugPortRequest2](../../extensibility/debugger/reference/idebugportrequest2.md)参数传递给[AddPort](../../extensibility/debugger/reference/idebugportsupplier2-addport.md)创建。

  [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]提供默认端口，用于处理所有基于 Windows 的进程，包括本机进程和托管进程。 必须为与非基于 Windows 的外部设备的连接设置自定义端口。 要提供此类自定义端口，还必须设置自定义端口供应商。

## <a name="see-also"></a>请参阅
- [服务器](../../extensibility/debugger/servers-visual-studio-sdk.md)
- [过程](../../extensibility/debugger/processes.md)
- [调试器概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md)
- [IDebugPortRequest2](../../extensibility/debugger/reference/idebugportrequest2.md)
- [AddPort](../../extensibility/debugger/reference/idebugportsupplier2-addport.md)
