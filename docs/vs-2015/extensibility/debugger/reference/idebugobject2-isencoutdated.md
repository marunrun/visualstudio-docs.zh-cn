---
title: IDebugObject2：： IsEncOutdated |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugObject2::IsEncOutdated
helpviewer_keywords:
- IDebugObject2::IsEncOutdated method
ms.assetid: d3a8c02d-895b-478c-9957-d663130f308e
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fa4acd0476a0df75644738840da562db97a34bf6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840462"
---
# <a name="idebugobject2isencoutdated"></a>IDebugObject2::IsEncOutdated
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此方法确定此对象或父容器的 "编辑并继续" 状态是否过时。 自定义表达式计算器不实现此方法并始终返回 `E_NOTIMPL` 。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT IsEncOutdated(  
   BOOL* pfEncOutdated  
);  
```  
  
```csharp  
int IsEncOutdated(  
   out int pfEncOutdated  
);  
```  
  
#### <a name="parameters"></a>parameters  
 `pfEncOutdated`  
 弄 `TRUE` 如果 "编辑并继续" 状态为 "过期"，则为非零 () ， `FALSE` 如果不是，则 () 。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
> [!NOTE]
> 自定义表达式计算器应该总是返回 `E_NOTIMPL` 。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)
