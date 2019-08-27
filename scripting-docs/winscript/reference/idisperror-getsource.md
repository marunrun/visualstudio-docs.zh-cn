---
title: IDispError::GetSource |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDispError.GetSource
apilocation:
- scrobj.dll
helpviewer_keywords:
- IDispError::GetSource
ms.assetid: 20def54c-a67c-4102-babf-6f0704e5fc5c
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8a84640f020a1ff255b8c7e5dd753752e0d310a7
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63446880"
---
# <a name="idisperrorgetsource"></a>IDispError::GetSource
返回的类或引发了错误的应用程序的依赖于语言的编程标识符。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetSource(  
   BSTR*  pbstrSource  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pbstrSource`  
 [out]字符串，其中包含窗体中的编程标识符`progname.objectname`。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 此方法用于确定类或应用程序发生异常。 指定在调用时提供的区域设置标识符 (LCID) 的语言中可能会返回的编程标识符。  
  
> [!NOTE]
> 未实现此方法。  
  
## <a name="see-also"></a>请参阅  
 [IDispError 接口](../../winscript/reference/idisperror-interface.md)