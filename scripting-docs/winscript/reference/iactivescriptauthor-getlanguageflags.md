---
title: IActiveScriptAuthor::GetLanguageFlags | Microsoft Docs
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
ms.openlocfilehash: d9f1a68db05ac0d909108ce77587ae4b071c9a2b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62935466"
---
# <a name="iactivescriptauthorgetlanguageflags"></a>IActiveScriptAuthor::GetLanguageFlags
返回语言的信息。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT GetLanguageFlags(  
   DWORD              *pgrfasa  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pgrfasa`  
 [out]包含语言信息的标志。 可以是以下值的组合：  
  
|返回的常量|“值”|描述|  
|--------------|-----------|-----------------|  
|fasaPreferInternalHandler|0x0001|语言更适合于创建脚本事件处理程序创建由脚本创作而不是应用程序的引擎。|  
|fasaSupportInternalHandler|0x0002|脚本事件处理程序创建的脚本创作引擎支持的语言。|  
|fasaCaseSensitive|0x0004|脚本语言是区分大小写。|  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
 如果脚本创作引擎管理事件处理程序，应用程序应调用`CreateChildHandler`从`IScriptEntry`对象。 这将创建`IScriptScriptlet`与事件处理程序对应的对象。 该引擎还将事件处理程序添加到脚本条目。 事件处理程序是一个空的函数，其中包含指定的签名信息。  
  
 如果应用程序管理事件处理程序，则应调用`CreateChildHandler`从`IScriptNode`对象，表示事件处理程序 scriptlet。 这将创建`IScriptScriptlet`与事件处理程序 scriptlet 相关联的对象。 应用程序还必须将一个空函数添加为事件处理程序到新的或现有的`IScriptEntry`对象。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptAuthor 接口](../../winscript/reference/iactivescriptauthor-interface.md)