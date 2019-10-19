---
title: IActiveScriptAuthor：： AddScriptlet |Microsoft Docs
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
ms.openlocfilehash: 3a349a848f282e6b3a228c7b17009e0261801be5
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72577974"
---
# <a name="iactivescriptauthoraddscriptlet"></a>IActiveScriptAuthor::AddScriptlet
将代码 scriptlet 添加为根级别 `IScriptNode` 对象的子对象。 在宿主中，允许 scriptlet 的完全限定名只有两个级别。  
  
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
 中要与 scriptlet 关联的默认名称的地址。  
  
 `pszCode`  
 中Scriptlet 文本的地址。  
  
 `pszItemName`  
 中主机中完全限定的 scriptlet 名称的顶级标识符的缓冲区地址。  
  
 `pszSubItemName`  
 中主机中完全限定的 scriptlet 名称的第二级标识符的缓冲区地址。 如果名称只有一个级别，则设置为 NULL。  
  
 `pszEventName`  
 中缓冲区的地址，该缓冲区包含 scriptlet 为其事件处理程序的事件名称。  
  
 `pszDelimiter`  
 中脚本结束分隔符的地址。 当从文本流分析 `pszCode` 时，主机通常使用分隔符（如两个单引号）来检测脚本块的结尾。 如果分隔符不标记脚本块的末尾，则将此参数设置为 NULL。  
  
 `dwCookie`  
 中应用程序定义的值，用于将 scriptlet 与主机对象相关联。  
  
 `dwFlags`  
 中不使用。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptAuthor 接口](../../winscript/reference/iactivescriptauthor-interface.md)