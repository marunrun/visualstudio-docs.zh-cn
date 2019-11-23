---
title: IScriptNode：： CreateChildHandler |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IScriptNode.CreateChildHandler
apilocation:
- scrobj.dll
helpviewer_keywords:
- IScriptNode::CreateChildHandler
ms.assetid: 4ce5eb10-1a3f-43b0-a4b7-599a397ed3a2
caps.latest.revision: 14
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 9e024bb7d6a81b35994edddfe9e71666b0ee8df0
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72573605"
---
# <a name="iscriptnodecreatechildhandler"></a>IScriptNode::CreateChildHandler
添加 scriptlet 作为 `IScriptNode`的子实例。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT CreateChildHandler(  
   LPCOLESTR          pszDefaultName,  
   LPCOLESTR          *prgpszNames,  
   ULONG              cpszNames,  
   LPCOLESTR          pszEvent,  
   LPCOLESTR          pszDelimiter,  
   ITypeInfo*         ptiSignature,  
   ULONG              iMethodSignature,  
   ULONG              isn,  
   DWORD              dwCookie,  
   IScriptEntry       **ppse  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pszDefaultName`  
 中要与 scriptlet 关联的默认名称的地址。  
  
 `prgpszNames`  
 [in，size_is （`cpszNames`）]主机上的完全限定名中的标识符列表。  
  
 `cpszNames`  
 中`prgpszNames` 参数中的标识符数量。  
  
 `pszEvent`  
 中标识与 scriptlet 关联的事件名称的缓冲区地址。  
  
 `pszDelimiter`  
 中脚本结束分隔符的地址。 为了进行分析，主机通常使用分隔符（如两个单引号）来检测脚本块的结尾。  
  
 分隔符允许脚本创作引擎进行预处理。 例如，引擎可以将带有两个单引号的单引号替换为分隔符。 引擎确定如何使用分隔符。  
  
 如果没有分隔符用于标识脚本块的末尾，则设置为 NULL。  
  
 `ptiSignature`  
 中函数对象的类型信息。  
  
 `iMethodSignature`  
 中`ITypeInfo``ptiSignature` 参数中函数的索引。  
  
 `isn`  
 中父中子级的索引。  
  
 `dwCookie`  
 中应用程序定义的值，用于将项与宿主对象相关联。  
  
 `ppse`  
 弄一个变量的地址，该变量接收指向子实例的 `IScriptEntry` 接口的指针。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|值|说明|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 Scriptlet 指定事件处理程序。 此方法会创建一个 scriptlet，如果它由表示网页的 `IScriptNode` 对象调用。 如果其他接口调用此方法，则此方法不会成功。  
  
## <a name="see-also"></a>另请参阅  
 [IScriptNode 接口](../../winscript/reference/iscriptnode-interface.md)   
 [IScriptEntry 接口](../../winscript/reference/iscriptentry-interface.md)