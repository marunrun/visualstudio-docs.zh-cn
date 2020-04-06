---
title: 实施端口供应商 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], implementing port suppliers
- port suppliers, implementing
ms.assetid: 6b8579df-58df-4c7f-8112-6015993e8765
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8218e372ad3aece922811bc20cfd7650f33296f3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738553"
---
# <a name="implement-a-port-supplier"></a>实施端口供应商
端口供应商应要求向会话调试管理器 （SDM） 提供端口。 调试到非 DCOM 计算机或新设备需要支持时，必须实现端口供应商。 例如，要向手机提供调试，可以设置一个端口供应商，该端口提供端口，这些端口连接到手机（可能通过 IR 或手机连接），并枚举在电话上运行的进程和程序。

 对于基于 Windows 的计算机上的调试程序（包括远程调试），Visual Studio 为本机和通用语言运行时 （CLR） 进程提供端口供应商，因此在这些情况下无需设置您自己的端口供应商。

## <a name="in-this-section"></a>在本节中
 [实施和注册端口供应商](../../extensibility/debugger/implementing-and-registering-a-port-supplier.md)讨论 SDM 如何与端口供应商及其端口进行交互。

 [所需的端口供应商接口](../../extensibility/debugger/required-port-supplier-interfaces.md)记录获取端口供应商时必须实现的接口。

## <a name="related-sections"></a>相关章节
 [调试器概念](../../extensibility/debugger/debugger-concepts.md)描述主要的调试体系结构概念。

## <a name="see-also"></a>请参阅
 [可视化工作室调试器可扩展性](../../extensibility/debugger/visual-studio-debugger-extensibility.md)
