---
title: IActiveScriptAuthor：： GetLanguageFlags |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptAuthor.GetLanguageFlags
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptAuthor::GetLanguageFlags
ms.assetid: eb244452-62f7-4a73-b48f-1aa05cbcc32d
caps.latest.revision: 14
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 68da16513050bd87642be2c96212a330a0916608
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576202"
---
# <a name="iactivescriptauthorgetlanguageflags"></a>IActiveScriptAuthor::GetLanguageFlags
返回语言信息。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetLanguageFlags(  
   DWORD              *pgrfasa  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pgrfasa`  
 弄包含语言信息的标志。 可以是以下值的组合：  
  
|返回的常量|“值”|描述|  
|--------------|-----------|-----------------|  
|fasaPreferInternalHandler|0x0001|该语言首选由脚本创作引擎（而不是应用程序）创建脚本事件处理程序。|  
|fasaSupportInternalHandler|0x0002|该语言支持脚本创作引擎创建的脚本事件处理程序。|  
|fasaCaseSensitive|0x0004|脚本语言区分大小写。|  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 如果脚本创作引擎管理事件处理程序，则应用程序应从 `IScriptEntry` 对象调用 `CreateChildHandler`。 这将创建一个与事件处理程序对应的 `IScriptScriptlet` 对象。 引擎还会将一个事件处理程序添加到脚本条目。 事件处理程序是一个空函数，其中包含指定的签名信息。  
  
 如果你的应用程序管理事件处理程序，它应从表示事件处理程序 scriptlet 的 `IScriptNode` 对象调用 `CreateChildHandler`。 这会创建与事件处理程序 scriptlet 关联的 `IScriptScriptlet` 对象。 应用程序还必须将空函数作为事件处理程序添加到新的或现有的 `IScriptEntry` 对象。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptAuthor 接口](../../winscript/reference/iactivescriptauthor-interface.md)