---
title: IActiveScriptSite：： GetDocVersionString |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptSite.GetDocVersionString
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptSite_GetDocVersionString
ms.assetid: ab3f892d-06d3-4cb5-9ea5-20c4a1e518cd
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8ecc592b6b7fcae5f516a3c1dd111c027e67b6dc
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72571130"
---
# <a name="iactivescriptsitegetdocversionstring"></a>IActiveScriptSite::GetDocVersionString
检索一个主机定义的字符串，该字符串唯一标识当前文档版本。 如果相关文档在 Windows 脚本范围外发生了更改（如使用记事本编辑 HTML 页的情况），则脚本引擎可以将其保存在持久性状态下，并在下次加载脚本时强制进行重新编译。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetDocVersionString(  
    BSTR *pbstrVersionString  // address of document version string  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pstrVersionString`  
 弄主机定义的文档版本字符串的地址。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`; 如果不支持此方法，则返回 `E_NOTIMPL`。  
  
## <a name="remarks"></a>备注  
 如果返回 `E_NOTIMPL`，则脚本引擎应假定脚本与文档同步。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)