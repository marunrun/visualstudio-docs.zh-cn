---
title: IScriptNode::CreateChildHandler | Microsoft Docs
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
ms.openlocfilehash: bca8b30021d39638f3755bace2625bb38a44242d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62787139"
---
# <a name="iscriptnodecreatechildhandler"></a>IScriptNode::CreateChildHandler
将作为子实例添加 scriptlet `IScriptNode`。  
  
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
 [in]若要将与 scriptlet 相关联的默认名称的地址。  
  
 `prgpszNames`  
 [在中，size_is (`cpszNames`)] 从主机上的完全限定名称的标识符的列表。  
  
 `cpszNames`  
 [in]中的标识符数`prgpszNames`参数。  
  
 `pszEvent`  
 [in]标识与 scriptlet 相关联的事件名称的缓冲区地址。  
  
 `pszDelimiter`  
 [in]最终的脚本块分隔符的地址。 有关分析过程中，主机通常使用分隔符 （如两个单引号），来检测脚本块的末尾。  
  
 分隔符，预处理脚本创作引擎。 例如，该引擎可能可用一个单引号将替换为使用用作分隔符的两个单引号。 在引擎确定如何使用分隔符。  
  
 如果没有分隔符用于标识脚本块的末尾，则设置为 NULL。  
  
 `ptiSignature`  
 [in]函数对象的类型信息。  
  
 `iMethodSignature`  
 [in]中的函数的索引`ITypeInfo``ptiSignature`参数。  
  
 `isn`  
 [in]子对象的父代中的索引。  
  
 `dwCookie`  
 [in]应用程序定义的一个值，用于将项与主机对象相关联。  
  
 `ppse`  
 [out]一个变量来接收指向指针的地址`IScriptEntry`接口的子实例。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 Scriptlet 指定事件处理程序。 如果调用此方法会创建 scriptlet`IScriptNode`对象，表示 Web 页。 如果通过其他接口调用此方法不成功。  
  
## <a name="see-also"></a>请参阅  
 [IScriptNode 接口](../../winscript/reference/iscriptnode-interface.md)   
 [IScriptEntry 接口](../../winscript/reference/iscriptentry-interface.md)