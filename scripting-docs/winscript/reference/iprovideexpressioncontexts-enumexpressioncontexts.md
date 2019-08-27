---
title: IProvideExpressionContexts::EnumExpressionContexts | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IProvideExpressionContexts.EnumExpressionContexts
apilocation:
- jscript.dll
helpviewer_keywords:
- IProvideExpressionContexts::EnumExpressionContexts
ms.assetid: ec5f0065-00df-41e6-b480-4c04ba464872
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 965147083bdc11a3544561fdd96cd85221ccd443
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63410153"
---
# <a name="iprovideexpressioncontextsenumexpressioncontexts"></a>IProvideExpressionContexts::EnumExpressionContexts
返回已知的此组件表达式上下文的枚举器。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT EnumExpressionContexts(  
   IEnumDebugExpressionContexts**  ppedec  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppedec`  
 [out]已知的此组件表达式上下文的一个枚举器。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 进程调试管理器使用此方法查找与给定线程关联的所有全局表达式上下文。  
  
> [!NOTE]
> 此方法是从内部所需的线程调用的。 它是由实现者确定当前线程，并返回相应的枚举器。  
  
## <a name="see-also"></a>请参阅  
 [IProvideExpressionContexts 接口](../../winscript/reference/iprovideexpressioncontexts-interface.md)