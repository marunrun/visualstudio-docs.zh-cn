---
title: IScriptNode：： CreateChildEntry |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IScriptNode. CreateChildEntry
apilocation:
- scrobj.dll
helpviewer_keywords:
- IScriptNode::CreateChildEntry
ms.assetid: b9682505-4457-40e9-8691-235843637506
caps.latest.revision: 17
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c58ff83c43a1418e6fb7bd8945afa181af60c68a
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72573606"
---
# <a name="iscriptnode-createchildentry"></a>IScriptNode:: CreateChildEntry
添加 `IScriptEntry`的子实例。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT CreateChildEntry(  
   ULONG              isn,  
   DWORD              dwCookie,  
   LPCOLESTR          pszDelimiter,  
   IScriptEntry       **ppse  
);  
```  
  
#### <a name="parameters"></a>参数  
 `isn`  
 中父中子级的索引。  
  
 `dwCookie`  
 中应用程序定义的值，用于将子条目与宿主对象相关联。  
  
 `pszDelimiter`  
 中脚本结束分隔符的地址。 为了进行分析，主机通常使用分隔符（如两个单引号）来检测脚本块的结尾。  
  
 此分隔符使脚本创作引擎能够提供预处理。 例如，引擎可以将带有两个单引号的单引号替换为分隔符。 引擎确定如何使用分隔符。  
  
 如果分隔符不标记脚本块的末尾，则设置为 NULL。  
  
 `ppse`  
 弄一个变量的地址，该变量接收指向子实例的 `IScriptEntry` 接口的指针。  
  
 对于表示网页的 `IScriptNode` 对象，此参数将返回指定脚本块的 `IScriptEntry` 实例。  
  
 对于表示脚本块的 `IScriptEntry` 对象，此参数返回指定函数对象的 `IScriptEntry` 实例。  
  
 对于表示函数对象的 `IScriptEntry` 对象，此方法将失败。  
  
 对于 `IScriptScriptlet` 对象，此方法将失败。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|值|说明|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 `IScriptNode` 接口表示网页或其元素。 `IScriptEntry` 接口（派生自 `IScriptNode`）表示脚本块或函数对象。 `IScriptScriptlet` 接口（派生自 `IScriptEntry`）表示事件处理程序。  
  
## <a name="see-also"></a>另请参阅  
 [IScriptNode 接口](../../winscript/reference/iscriptnode-interface.md)   
 [IScriptEntry 接口](../../winscript/reference/iscriptentry-interface.md)