---
title: IDispError::GetHelpInfo | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDispError.GetHelpInfo
apilocation:
- scrobj.dll
helpviewer_keywords:
- IDispError::GetHelpInfo
ms.assetid: a146df13-eda4-4e56-8bf0-cf9886a2150f
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: fa831ff511ea507e03ca858b93383ff38ead9039
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63446907"
---
# <a name="idisperrorgethelpinfo"></a>IDispError::GetHelpInfo
返回的帮助文件的路径和解释该错误，如有可能的主题的上下文 ID。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetHelpInfo(  
   BSTR*  pbstrFileName,  
   DWORD*  pdwContext  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pbstrFileName`  
 [out]包含帮助文件的完全限定的路径的字符串。 如果没有帮助文件或者出现错误，则返回值为 NULL。  
  
 `pdwContext`  
 [out]错误的帮助上下文 ID。 如果没有帮助文件 (如果`pbstrFileName`为 NULL)，此参数没有任何意义。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
|`E_FAIL`|发生了特定于提供程序的错误。|  
|`E_INVALIDARG`|`pbstrFileName` 或`pdwContext`为 NULL。|  
|`E_OUTOFMEMORY`|提供程序无法分配足够的内存用于返回的帮助文件路径。|  
  
## <a name="remarks"></a>备注  
 此方法返回的帮助文件的路径和解释该错误，如有可能的主题的上下文 ID。  
  
> [!NOTE]
> 未实现此方法。  
  
## <a name="see-also"></a>请参阅  
 [IDispError 接口](../../winscript/reference/idisperror-interface.md)