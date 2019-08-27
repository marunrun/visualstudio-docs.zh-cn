---
title: IEnumDebugCodeContexts2::Reset |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEnumDebugCodeContexts2::Reset
helpviewer_keywords:
- IEnumDebugCodeContexts2::Reset
ms.assetid: df6cf1e3-2ef8-4d38-81a0-8e9adf151884
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 284c8c4b50813fbdeb6decf4f1a9bd4b73a168e2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68158099"
---
# <a name="ienumdebugcodecontexts2reset"></a>IEnumDebugCodeContexts2::Reset
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

将枚举重置为第一个元素。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Reset(  
   void  
);  
```  
  
```csharp  
int Reset();  
```  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 调用此方法下, 一步调用后[下一步](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-next.md)方法返回的第一个元素的枚举。  
  
## <a name="see-also"></a>请参阅  
 [IEnumDebugCodeContexts2](../../../extensibility/debugger/reference/ienumdebugcodecontexts2.md)
