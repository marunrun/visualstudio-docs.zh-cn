---
title: 实现端口提供程序 |Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68152674"
---
# <a name="implementing-a-port-supplier"></a>实现端口提供程序
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

端口提供程序提供对会话调试管理器 (SDM) 请求上的端口。 需要调试到非 DCOM 计算机时或当需要支持新的设备实现端口提供程序。 例如，若要提供对移动电话调试，您可以实现端口提供程序提供端口 （也许是通过红外线 （ir） 或单元格连接） 连接到移动电话和枚举的过程和程序在手机上运行的任务。  
  
 对于基于 Windows 的计算机 （包括远程调试） 上的调试程序，Visual Studio 提供端口供应商的本机和公共语言运行时 (CLR) 的进程，因此无需在这些情况下实现您自己的端口提供程序。  
  
## <a name="in-this-section"></a>本节内容  
 [实现和注册端口提供程序](../../extensibility/debugger/implementing-and-registering-a-port-supplier.md)  
 讨论 SDM 与端口提供程序和其端口交互的方式。  
  
 [所需的端口提供程序接口](../../extensibility/debugger/required-port-supplier-interfaces.md)  
 文档必须实现以获取端口提供程序的接口。  
  
## <a name="related-sections"></a>相关章节  
 [调试器概念](../../extensibility/debugger/debugger-concepts.md)  
 描述调试的主要体系结构概念。  
  
## <a name="see-also"></a>请参阅  
 [Visual Studio 调试器可扩展性](../../extensibility/debugger/visual-studio-debugger-extensibility.md)
