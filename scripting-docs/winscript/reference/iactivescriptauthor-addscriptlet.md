---
title: IActiveScriptAuthor::AddScriptlet | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptAuthor.AddScriptlet
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptAuthor::AddScriptlet
ms.assetid: 879a6651-f187-4934-b130-c1247549900b
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 64df7bd4c0d0dde303cdc15d7111688d14c7dc49
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62935453"
---
# <a name="iactivescriptauthoraddscriptlet"></a>IActiveScriptAuthor::AddScriptlet
将作为根级别的子级添加的代码 scriptlet`IScriptNode`对象。 在宿主中，允许 scriptlet 的完全限定的名称具有只有两个级别。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT AddScriptlet(  
   LPCOLESTR pszDefaultName,  
   LPCOLESTR pszCode,  
   LPCOLESTR pszItemName,  
   LPCOLESTR pszSubItemName,  
   LPCOLESTR pszEventName,  
   LPCOLESTR pszDelimiter,  
   DWORD dwCookie,  
   DWORD dwFlags  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pszDefaultName`  
 [in]若要将与 scriptlet 相关联的默认名称的地址。  
  
 `pszCode`  
 [in]Scriptlet 文本的地址。  
  
 `pszItemName`  
 [in]顶级标识符中主机的完全限定的 scriptlet 名称的缓冲区地址。  
  
 `pszSubItemName`  
 [in]在主机中的完全限定的 scriptlet 名称的第二级别标识符的缓冲区地址。 如果名称只有一个级别，则设置为 NULL。  
  
 `pszEventName`  
 [in]包含为其 scriptlet 是一个事件处理程序的事件名称的缓冲区的地址。  
  
 `pszDelimiter`  
 [in]最终的脚本块分隔符的地址。 当`pszCode`进行分析的文本流，从主机通常使用分隔符 （如两个单引号），来检测脚本块的末尾。 如果分隔符将脚本块的末尾不标记，此参数设置为 NULL。  
  
 `dwCookie`  
 [in]应用程序定义的一个值，用于将 scriptlet 与主机对象相关联。  
  
 `dwFlags`  
 [in]不使用。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptAuthor 接口](../../winscript/reference/iactivescriptauthor-interface.md)