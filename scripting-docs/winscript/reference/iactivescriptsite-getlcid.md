---
title: IActiveScriptSite：： GetLCID |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptSite.GetLCID
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptSite_GetLCID
ms.assetid: 7b4a2dc1-bcf6-4bbf-884e-97b305a28eb7
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 913ca23ac687fdd080a778afb1dcba2e4dcdd6b8
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72570735"
---
# <a name="iactivescriptsitegetlcid"></a>IActiveScriptSite::GetLCID
检索与宿主的用户界面相关联的区域设置标识符。 脚本引擎使用标识符来确保引擎生成的错误字符串和其他用户界面元素以适当的语言显示。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetLCID(  
    LCID *plcid  // address of variable for language identifier  
);  
```  
  
#### <a name="parameters"></a>参数  
 `plcid`  
 弄变量的地址，该变量接收脚本引擎显示的用户界面元素的区域设置标识符。  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|成功。|  
|`E_NOTIMPL`|未实现此方法。 使用系统定义的区域设置。|  
|`E_POINTER`|指定的指针无效。|  
  
## <a name="remarks"></a>备注  
 如果此方法返回 `E_NOTIMPL`，则应使用系统定义的区域设置标识符。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)