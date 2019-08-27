---
title: IDebugPortSupplierEx2 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugPortSupplierEx2 interface
ms.assetid: dae0050a-a50a-4f35-bfbd-e538f537b20f
caps.latest.revision: 5
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e59d3eb67fe45003babf53862736a435586deeeb
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62537935"
---
# <a name="idebugportsupplierex2"></a>IDebugPortSupplierEx2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

为端口提供程序选择并核心服务器与之交互提供支持。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugPortSupplierEx2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 自定义端口提供程序实现此接口，以便它可以选择要使用的核心服务器。  
  
## <a name="methods"></a>方法  
 下表显示的方法**IDebugPortSupplierEx2**。  
  
|方法|描述|  
|------------|-----------------|  
|[SetServer](../../../extensibility/debugger/reference/idebugportsupplierex2-setserver.md)|设置端口提供程序的核心服务器。|  
  
## <a name="requirements"></a>要求  
 标头：Portpriv.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)   
 [IDebugPortSupplier3](../../../extensibility/debugger/reference/idebugportsupplier3.md)
