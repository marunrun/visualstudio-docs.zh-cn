---
title: IDebugThread2::EnumFrameInfo |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugThread2::EnumFrameInfo
helpviewer_keywords:
- IDebugThread2::EnumFrameInfo
ms.assetid: 17914a71-10ea-4b6f-8982-e364f87dca53
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: efda31daae198befbda35803ef71e1d0322e9bbd
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68153087"
---
# <a name="idebugthread2enumframeinfo"></a>IDebugThread2::EnumFrameInfo
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

检索此线程的堆栈帧的列表。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT EnumFrameInfo (   
   FRAMEINFO_FLAGS        dwFieldSpec,  
   UINT                   nRadix,  
   IEnumDebugFrameInfo2** ppEnum  
);  
```  
  
```csharp  
int EnumFrameInfo (   
   enum_FRAMEINFO_FLAGS     dwFieldSpec,  
   uint                     nRadix,  
   out IEnumDebugFrameInfo2 ppEnum  
);  
```  
  
#### <a name="parameters"></a>参数  
 `dwFieldSpec`  
 [in]中的标志的组合[FRAMEINFO_FLAGS](../../../extensibility/debugger/reference/frameinfo-flags.md)枚举，用于指定的哪些字段[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)结构是要填写。指定`FIF_FUNCNAME_FORMAT`标志设置为一个字符串的格式的函数名称。  
  
 `nRadix`  
 [in]设置格式的枚举数中的数字信息时使用的基数。  
  
 `ppEnum`  
 [out]返回[IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)对象，其中包含一系列[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)结构描述的堆栈帧。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 使用第一次枚举的当前帧和上一次枚举的最早帧中顺序，列举了线程的帧。  
  
## <a name="see-also"></a>请参阅  
 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)   
 [FRAMEINFO_FLAGS](../../../extensibility/debugger/reference/frameinfo-flags.md)   
 [IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)   
 [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)
