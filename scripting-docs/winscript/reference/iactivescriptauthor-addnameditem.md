---
title: IActiveScriptAuthor::AddNamedItem | Microsoft Docs
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
ms.openlocfilehash: 95bc529db8129c4e9af1ed9f9dc3d91de9686223
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63411390"
---
# <a name="iactivescriptauthoraddnameditem"></a>IActiveScriptAuthor::AddNamedItem
将根级别项的名称添加到引擎的命名空间创作的脚本。 一个*根级别项*是包含属性和方法，并且，还可以包含事件源的对象。  
  
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
 [in]从脚本来查看的项的名称。 名称必须唯一且可持久化。  
  
 `dwFlags`  
 [in]与命名项关联的标志。 可以是以下值的组合：  
  
|返回的常量|“值”|描述|  
|--------------|-----------|-----------------|  
|SCRIPTITEM_ISVISIBLE|0x00000002|指示项的名称是脚本的命名空间中可用。 这允许访问项的属性、 方法和事件。<br /><br /> 按照约定，项的属性包括项的子成员。 因此，所有子对象属性和方法 （和自身的子成员，以递归方式） 进行访问。|  
|SCRIPTITEM_ISSOURCE|0x00000004|指示该脚本可以具有脚本事件处理程序的项目源的事件。|  
|SCRIPTITEM_GLOBALMEMBERS|0x00000008|指示该项全局属性和方法以与脚本关联的集合。 其成员被编写为全局变量和方法。|  
|SCRIPTITEM_ISPERSISTENT|0x00000040|指示是否保存脚本创作引擎应保存该项。|  
|SCRIPTITEM_CODEONLY|0x00000200|指示命名的项表示仅限代码的对象，并且它不具有成员来创作。|  
|SCRIPTITEM_NOCODE|0x00000400|指示命名的项是要添加的名称，并且没有要创作。|  
  
 `pdisp`  
 [in]`IDispatch`的`NamedItem`用于收集方法、 属性或事件源的对象。  
  
## <a name="return-value"></a>返回值  
 一个 `HRESULT`。 可能的值包括（但并不限于）下表中的项。  
  
|“值”|描述|  
|-----------|-----------------|  
|`S_OK`|方法成功。|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [IActiveScriptAuthor 接口](../../winscript/reference/iactivescriptauthor-interface.md)   
 [IActiveScriptAuthor::RemoveNamedItem](../../winscript/reference/iactivescriptauthor-removenameditem.md)