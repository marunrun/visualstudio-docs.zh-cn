---
title: IDebugBreakpointChecksumRequest2 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugBreakpointChecksumRequest2 interface
ms.assetid: 9cfdbca5-052c-48e9-8411-e2e9e4065d00
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9d06656ba05c3356d9f2a148045adbf4538c5ae5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62431597"
---
# <a name="idebugbreakpointchecksumrequest2"></a>IDebugBreakpointChecksumRequest2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

表示断点请求的文档校验和。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugBreakpointChecksumRequest2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 实现的[!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]调试包和已使用的调试引擎。  
  
## <a name="methods"></a>方法  
 下表显示的方法`IDebugBreakpointChecksumRequest2`。  
  
|方法|描述|  
|------------|-----------------|  
|[GetChecksum](../../../extensibility/debugger/reference/idebugbreakpointchecksumrequest2-getchecksum.md)|检索给定的校验和算法的唯一标识符的断点请求使用的文档校验和。|  
|[IsChecksumEnabled](../../../extensibility/debugger/reference/idebugbreakpointchecksumrequest2-ischecksumenabled.md)|确定是否为本文档中启用了校验和。|  
  
## <a name="requirements"></a>要求  
 标头：Msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll
