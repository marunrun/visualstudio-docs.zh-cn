---
title: IScriptNode::CreateChildEntry |Microsoft Docs
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
ms.openlocfilehash: 75369df719b0cd140ce621e916215eb18cf30a9e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62787614"
---
# <a name="iscriptnode-createchildentry"></a>IScriptNode::CreateChildEntry
添加的子实例`IScriptEntry`。  
  
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
 [in]子对象的父代中的索引。  
  
 `dwCookie`  
 [in]应用程序定义的值，用于将子条目与主机对象相关联。  
  
 `pszDelimiter`  
 [in]最终的脚本块分隔符的地址。 有关分析过程中，主机通常使用分隔符 （如两个单引号），来检测脚本块的末尾。  
  
 分隔符可以创作引擎提供预处理脚本。 例如，该引擎可能可用一个单引号将替换为使用用作分隔符的两个单引号。 在引擎确定如何使用分隔符。  
  
 如果分隔符将脚本块的末尾不标记，设置为 NULL。  
  
 `ppse`  
 [out]一个变量来接收指向指针的地址`IScriptEntry`接口的子实例。  
  
 有关`IScriptNode`表示 Web 页的对象，此参数返回`IScriptEntry`指定脚本块的实例。  
  
 有关`IScriptEntry`对象表示脚本块，此参数返回`IScriptEntry`指定的函数对象的实例。  
  
 有关`IScriptEntry`对象表示一个函数的对象，此方法将失败。  
  
 有关`IScriptScriptlet`对象，此方法将失败。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 `IScriptNode`接口表示 Web 页或它的元素。 `IScriptEntry`接口 (它派生自`IScriptNode`) 表示的脚本块或函数对象。 `IScriptScriptlet`接口 (它派生自`IScriptEntry`) 表示一个事件处理程序。  
  
## <a name="see-also"></a>请参阅  
 [IScriptNode 接口](../../winscript/reference/iscriptnode-interface.md)   
 [IScriptEntry 接口](../../winscript/reference/iscriptentry-interface.md)