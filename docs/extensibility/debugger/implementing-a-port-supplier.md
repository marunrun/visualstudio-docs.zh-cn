---
title: 实现端口供应商 |Microsoft Docs
description: 了解如何实现端口供应商，在对非 DCOM 计算机进行调试或者新设备需要支持时，这是必需的。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 72963660e4f50a72cdbc04bab4833b397d15fc27
ms.sourcegitcommit: bbed6a0b41ac4c4a24e8581ff3b34d96345ddb00
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2020
ms.locfileid: "96560663"
---
# <a name="implement-a-port-supplier"></a>实现端口供应商
端口供应商向会话调试管理器 (SDM) 提供请求端口。 当调试到非 DCOM 计算机或新设备需要支持时，必须实现端口供应商。 例如，若要为手机提供调试，你可以设置一个端口提供程序，该提供程序通过 IR 或单元连接) 连接到手机 (，并枚举在手机上运行的进程和程序。

 对于基于 Windows 的计算机上的调试程序 (包括远程调试) ，Visual Studio 为本机和公共语言运行时 (CLR) 进程提供端口提供程序，因此不需要在这些情况下设置你自己的端口供应商。

## <a name="in-this-section"></a>在本节中
 [实现并注册端口供应商](../../extensibility/debugger/implementing-and-registering-a-port-supplier.md) 讨论 SDM 如何与端口提供商及其端口交互。

 [必需的端口提供商接口](../../extensibility/debugger/required-port-supplier-interfaces.md) 记录为获取端口供应商而必须实现的接口。

## <a name="related-sections"></a>相关章节
 [调试器概念](../../extensibility/debugger/debugger-concepts.md) 介绍主要的调试体系结构概念。

## <a name="see-also"></a>另请参阅
 [Visual Studio 调试器扩展性](../../extensibility/debugger/visual-studio-debugger-extensibility.md)
