---
title: 港口供应商 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- port suppliers
- debugging [Debugging SDK], port suppliers
ms.assetid: a8f3db96-1a13-4e93-9ef6-0861880369e0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6313a7afce9ed272177a26d8da1a9d1516c8022e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738294"
---
# <a name="port-suppliers"></a>港口供应商
在调试器体系结构中，*端口供应商*：

- 由服务器控制，并应请求向该服务器提供端口。

- 可以从包含的服务器添加和删除端口。

- 可以枚举它提供给服务器的所有端口。

- 由[IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md)接口表示，该接口通过注册表在 Visual Studio 中注册。 此接口可以通过调用[GetPortSupplier](../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md)获得。

  [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]提供默认端口供应商和默认端口。 如果需要实现自定义端口，还需要实施自定义端口供应商来提供这些自定义端口。

## <a name="see-also"></a>请参阅
- [服务器](../../extensibility/debugger/servers-visual-studio-sdk.md)
- [港口](../../extensibility/debugger/ports.md)
- [调试器概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md)
- [GetPortSupplier](../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md)
