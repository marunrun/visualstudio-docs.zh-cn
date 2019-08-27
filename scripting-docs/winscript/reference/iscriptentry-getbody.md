---
title: IScriptEntry::GetBody | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IScriptEntry.GetBody
apilocation:
- scrobj.dll
helpviewer_keywords:
- IScriptEntry::GetBody
ms.assetid: 419c8c11-a1f8-4b97-ab00-e8af2b2f9bfc
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7f8f1ad24660401d575af2724b788387fd546af8
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62787874"
---
# <a name="iscriptentrygetbody"></a>IScriptEntry::GetBody
返回对应的文本正文的`IScriptEntry`脚本块、 函数块或 scriptlet。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetBody(  
   BSTR               *pbstr  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pbstr`  
 [out]在以下项之一的正文中的文本：  
  
- `IScriptEntry`脚本块  
  
- `IScriptEntry`函数块中的函数  
  
- `IScriptEntry` Scriptlet 事件处理程序  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [IScriptEntry 接口](../../winscript/reference/iscriptentry-interface.md)