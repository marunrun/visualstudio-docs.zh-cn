---
title: IScriptEntry：： GetRange |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IScriptEntry.GetRange
apilocation:
- scrobj.dll
helpviewer_keywords:
- IScriptEntry::GetRange
ms.assetid: 3ac18f0a-b470-4f4d-b8f5-2da3fdef74f1
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0a6e1b1600c93aa05bbe9669fb57a23a8c9344a1
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575438"
---
# <a name="iscriptentrygetrange"></a>IScriptEntry::GetRange
返回项的开始位置和长度。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetRange(  
   ULONG              *pichMin  
   ULONG              *pcch  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pichMin`  
 弄对于指定脚本块的 `IScriptEntry` 对象，将返回0。  
  
 对于指定函数对象 `IScriptEntry` 对象，返回函数在当前脚本块中的开始位置。  
  
 对于 `IScriptScriptlet` 对象，返回0。  
  
 `pcch`  
 弄对于指定脚本块的 `IScriptEntry` 对象，返回文本的长度。  
  
 对于指定函数对象 `IScriptEntry` 对象，返回函数定义的长度。  
  
 对于 `IScriptScriptlet` 对象，返回条目的长度。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [IScriptEntry 接口](../../winscript/reference/iscriptentry-interface.md)