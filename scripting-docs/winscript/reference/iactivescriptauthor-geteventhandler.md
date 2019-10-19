---
title: IActiveScriptAuthor：： GetEventHandler |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptAuthor.GetEventHandler
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptAuthor::GetEventHandler
ms.assetid: 87c7a71d-46b9-448c-b34d-394105e20982
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c69b32f0040ea6d52e0712b8e1813cc5a0b40c58
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72576219"
---
# <a name="iactivescriptauthorgeteventhandler"></a>IActiveScriptAuthor::GetEventHandler
返回具有指定特性的 scriptlet。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetEventHandler(  
   IDispatch          *pdisp,  
   LPCOLESTR          pszItem,  
   LPCOLESTR          pszSubItem,  
   LPCOLESTR          pszEvent,  
   IScriptEntry       **ppse  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pdisp`  
 中与 scriptlet 附加到的 `NamedItem` 对应的 `IDispatch` 对象。  
  
 `pszItem`  
 中主机中完全限定的 scriptlet 名称的顶级标识符的缓冲区地址。  
  
 `pszSubItem`  
 中主机中完全限定的 scriptlet 名称的第二级标识符的缓冲区地址。 如果名称只有一个级别，则设置为 NULL。  
  
 `pszEvent`  
 中包含事件名称的缓冲区的地址。 Scriptlet 是此事件的事件处理程序。  
  
 `ppse`  
 弄一个变量的地址，该变量接收指向具有指定属性的 scriptlet 的 `IScriptEntry` 接口的指针。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptAuthor 接口](../../winscript/reference/iactivescriptauthor-interface.md)   
 [IScriptEntry 接口](../../winscript/reference/iscriptentry-interface.md)