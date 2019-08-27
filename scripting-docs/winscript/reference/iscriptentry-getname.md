---
title: IScriptEntry::GetName | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IScriptEntry.GetName
apilocation:
- scrobj.dll
helpviewer_keywords:
- IScriptEntry::GetName
ms.assetid: 56daa288-618f-497c-a360-7d443afd478b
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d23843aa72ce5cf79f6442048b6493d17eb6ef64
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62787765"
---
# <a name="iscriptentrygetname"></a>IScriptEntry::GetName
对于表示单个对象 （如某个函数） 的条目，返回的对象的名称。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetName(  
   BSTR               *pbstr  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pbstr`  
 [out]所表示的对象的名称`IScriptEntry`脚本块。 如果输入不表示单个对象，则返回 NULL。  
  
 子条目都代表一个函数对象。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [IScriptEntry 接口](../../winscript/reference/iscriptentry-interface.md)   
 [IScriptNode::CreateChildEntry](../../winscript/reference/iscriptnode-createchildentry.md)