---
title: 端口 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- ports
- debugging [Debugging SDK], ports
ms.assetid: 1d7f3aa7-7eff-4cab-bc53-0a566b1a9363
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 73003e00fef5c37db4a702e7a4a1121600673844
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153691"
---
# <a name="ports"></a>端口
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

就调试器体系结构而言， **端口**：  
  
- 是一组在服务器上运行的进程的容器。 例如，端口可能表示通过串行电缆连接到基于 Windows CE 的设备，或连接到联网的非 DCOM 计算机。 一个专用端口称为 "本地端口"，其中包含在本地计算机上运行的所有进程。  
  
- 可以按名称或标识符来标识自身。  
  
- 可枚举端口上运行的所有进程，并启动和终止这些进程。  
  
- 由 [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md) 接口表示，该接口通过将 [IDebugPortRequest2](../../extensibility/debugger/reference/idebugportrequest2.md) 参数传递给 [AddPort](../../extensibility/debugger/reference/idebugportsupplier2-addport.md)来创建。  
  
  [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 提供处理所有基于 Windows 的进程（本机和托管）的默认端口。 对于与不基于 Windows 的外部设备的连接，必须实现自定义端口。 若要提供此类自定义端口，还需要实现自定义端口供应商。  
  
## <a name="see-also"></a>另请参阅  
 [服务器](../../extensibility/debugger/servers-visual-studio-sdk.md)   
 [工艺](../../extensibility/debugger/processes.md)   
 [调试器概念](../../extensibility/debugger/debugger-concepts.md)   
 [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md)   
 [IDebugPortRequest2](../../extensibility/debugger/reference/idebugportrequest2.md)   
 [AddPort](../../extensibility/debugger/reference/idebugportsupplier2-addport.md)
