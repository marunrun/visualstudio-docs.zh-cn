---
title: IActiveScriptAuthor：： AddNamedItem |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptAuthor.AddNamedItem
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptAuthor::AddNamedItem
ms.assetid: 951003b6-1c4a-4086-b7ce-2f128e007280
caps.latest.revision: 19
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f0d2f08a49fdc768e87152bf486ce48687c79e68
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72577247"
---
# <a name="iactivescriptauthoraddnameditem"></a>IActiveScriptAuthor::AddNamedItem
将根级别项的名称添加到脚本创作引擎的命名空间中。 *根级别项*是一个对象，它可以包含属性和方法，还可以包含事件源。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT AddNamedItem(  
   LPCOLESTR          pszName,  
   DWORD              dwFlags,  
   IDispatch          *pdisp  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pszName`  
 中从脚本中查看的项的名称。 该名称必须唯一且可持久。  
  
 `dwFlags`  
 中与已命名项关联的标志。 可以是以下值的组合：  
  
|常量|值|说明|  
|--------------|-----------|-----------------|  
|SCRIPTITEM_ISVISIBLE|0x00000002|指示项的名称在脚本的命名空间中可用。 这允许访问项的属性、方法和事件。<br /><br /> 按照约定，项的属性包括项的子成员。 因此，所有子对象属性和方法（及其子成员递归）都是可访问的。|  
|SCRIPTITEM_ISSOURCE|0x00000004|指示该脚本可以具有脚本事件处理程序的项源事件。|  
|SCRIPTITEM_GLOBALMEMBERS|0x00000008|指示项是与脚本关联的全局属性和方法的集合。 它的成员作为全局变量和方法进行编写。|  
|SCRIPTITEM_ISPERSISTENT|0x00000040|指示在保存脚本创作引擎时应保存项。|  
|SCRIPTITEM_CODEONLY|0x00000200|指示已命名的项表示仅限代码的对象，并且它没有要创作的成员。|  
|SCRIPTITEM_NOCODE|0x00000400|指示已命名项仅为正在添加的名称，并且没有任何要创作的项。|  
  
 `pdisp`  
 中用于收集方法、属性或事件源的 `NamedItem` 对象的 `IDispatch`。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|值|说明|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [IActiveScriptAuthor 接口](../../winscript/reference/iactivescriptauthor-interface.md)   
 [IActiveScriptAuthor::RemoveNamedItem](../../winscript/reference/iactivescriptauthor-removenameditem.md)