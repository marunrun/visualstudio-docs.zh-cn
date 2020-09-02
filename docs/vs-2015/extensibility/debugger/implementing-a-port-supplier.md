---
title: 实现端口供应商 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], implementing port suppliers
- port suppliers, implementing
ms.assetid: 6b8579df-58df-4c7f-8112-6015993e8765
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ffa6daa20c08bd236657c88e762b2f453554cb74
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68152674"
---
# <a name="implementing-a-port-supplier"></a>实现端口提供程序
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

端口供应商向会话调试管理器 (SDM) 提供请求端口。 当调试到非 DCOM 计算机或需要支持新设备时，需要实现端口供应商。 例如，若要为手机提供调试，你可以实现一个端口提供程序，该提供程序提供连接到手机 (（可能通过 IR 或单元) 连接方式）的端口，并枚举在手机上运行的进程和程序。  
  
 对于基于 Windows 的计算机上的调试程序 (包括远程调试) ，Visual Studio 为本机和公共语言运行时 (CLR) 进程提供端口提供程序，因此不需要在这些情况下实现自己的端口供应商。  
  
## <a name="in-this-section"></a>本节内容  
 [实现和注册端口提供程序](../../extensibility/debugger/implementing-and-registering-a-port-supplier.md)  
 讨论 SDM 如何与端口提供商及其端口交互。  
  
 [所需的端口提供程序接口](../../extensibility/debugger/required-port-supplier-interfaces.md)  
 记录为获取端口提供程序而必须实现的接口。  
  
## <a name="related-sections"></a>相关章节  
 [调试器概念](../../extensibility/debugger/debugger-concepts.md)  
 介绍主要调试体系结构概念。  
  
## <a name="see-also"></a>另请参阅  
 [Visual Studio 调试器可扩展性](../../extensibility/debugger/visual-studio-debugger-extensibility.md)
