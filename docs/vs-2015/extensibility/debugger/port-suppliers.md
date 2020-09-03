---
title: 端口供应商 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- port suppliers
- debugging [Debugging SDK], port suppliers
ms.assetid: a8f3db96-1a13-4e93-9ef6-0861880369e0
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e90871927c30399dea4691381baa749db2b3e8bf
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153705"
---
# <a name="port-suppliers"></a>端口提供程序
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

就调试器体系结构而言， **端口供应商**：  
  
- 包含在服务器中，并提供对该服务器的请求的端口。  
  
- 可以在包含服务器中添加和删除端口。  
  
- 可以枚举它提供给服务器的所有端口。  
  
- 由 [IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md) 接口表示，该接口通过注册表向 Visual Studio 注册。 此接口可通过调用 [GetPortSupplier](../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md)获取。  
  
  [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 提供默认端口供应商和默认端口。 如果需要实现自定义端口，还需要实现自定义端口提供商以提供这些自定义端口。  
  
## <a name="see-also"></a>另请参阅  
 [服务器](../../extensibility/debugger/servers-visual-studio-sdk.md)   
 [端口](../../extensibility/debugger/ports.md)   
 [调试器概念](../../extensibility/debugger/debugger-concepts.md)   
 [IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md)   
 [GetPortSupplier](../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md)
