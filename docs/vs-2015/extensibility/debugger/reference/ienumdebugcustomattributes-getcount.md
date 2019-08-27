---
title: IEnumDebugCustomAttributes::GetCount |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEnumCustomAttributes::GetCount
helpviewer_keywords:
- IEnumDebugCustomAttributes::GetCount
ms.assetid: fafe826f-4ebf-4572-b2a3-d5dd2916c12f
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9c175297bf0f80c74e0c3409843164e0b08589ef
ms.sourcegitcommit: da4079f5b6ec884baf3108cbd0519d20cb64c70b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "62551486"
---
# <a name="ienumdebugcustomattributesgetcount"></a>IEnumDebugCustomAttributes::GetCount
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

获取一个枚举器中的自定义属性的数目。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetCount(   
   ULONG* pcelt  
);  
```  
  
```csharp  
int GetCount(  
   out uint pcelt  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pcelt`  
 [out]枚举中返回元素的数。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 此方法不是惯用的 COM 枚举接口，只有指定的一部分`Next`， `Clone`， `Skip`，和`Reset`需要实现。  
  
## <a name="see-also"></a>请参阅  
 [IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md)
