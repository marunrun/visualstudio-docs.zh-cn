---
title: IDebugField::Equal |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugField::Equal
helpviewer_keywords:
- IDebugField::Equal method
ms.assetid: 75369fe6-ddd3-497d-80d1-2488e6100e9f
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: aa630a6f2084f7ff79a9c89b685658cf694fcab9
ms.sourcegitcommit: 0cd282a7584b9bfd4df7882f8fdf3ad8a270e219
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2019
ms.locfileid: "62547307"
---
# <a name="idebugfieldequal"></a>IDebugField::Equal
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此方法将此字段与指定字段相等进行比较。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Equal(   
   IDebugField* pField  
);  
```  
  
```csharp  
int Equal(  
   IDebugField pField  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pField`  
 [in]要与此比较的字段。  
  
## <a name="return-value"></a>返回值  
 如果字段是相同的则返回`S_OK`。 如果字段不同，返回`S_FALSE.`否则，返回错误代码。  
  
## <a name="see-also"></a>请参阅  
 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
