---
title: IDispError：： GetHelpInfo |Microsoft Docs
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
ms.openlocfilehash: a84e57e97bb781ad3ea0be1ac6766fd94f6f5c30
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72573130"
---
# <a name="idisperrorgethelpinfo"></a>IDispError::GetHelpInfo
返回帮助文件的路径和说明错误的主题的上下文 ID （如果可能）。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetHelpInfo(  
   BSTR*  pbstrFileName,  
   DWORD*  pdwContext  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pbstrFileName`  
 弄包含帮助文件的完全限定路径的字符串。 如果没有帮助文件或出现错误，则返回值为 NULL。  
  
 `pdwContext`  
 弄错误的帮助上下文 ID。 如果没有帮助文件（如果 `pbstrFileName` 为 NULL），则此参数无意义。  
  
## <a name="return-value"></a>返回值  
 该方法返回 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
|`E_FAIL`|出现特定于提供程序的错误。|  
|`E_INVALIDARG`|`pbstrFileName` 或 `pdwContext` 为 NULL。|  
|`E_OUTOFMEMORY`|提供程序无法分配足够的内存来返回帮助文件路径。|  
  
## <a name="remarks"></a>备注  
 此方法返回帮助文件的路径和说明错误的主题的上下文 ID （如果可能）。  
  
> [!NOTE]
> 未实现此方法。  
  
## <a name="see-also"></a>请参阅  
 [IDispError 接口](../../winscript/reference/idisperror-interface.md)