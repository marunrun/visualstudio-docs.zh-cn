---
title: IActiveScript：： AddNamedItem |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScript.AddNamedItem
apilocation:
- scrobj.dll
helpviewer_keywords:
- AddNamedItem method, IActiveScript interface
ms.assetid: a7c6317d-948f-4bb3-b169-1bbe5b7c7cc5
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a343e38b944ca36da221da39832046c19b332230
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575824"
---
# <a name="iactivescriptaddnameditem"></a>IActiveScript::AddNamedItem
将根级别项的名称添加到脚本引擎的命名空间中。 根级别项是具有属性和方法的对象、事件源或全部三项。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT AddNamedItem(  
    LPCOLESTR pstrName,  // address of item name  
    DWORD dwFlags          // item flags  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pstrName`  
 中缓冲区的地址，其中包含从脚本中查看的项的名称。 该名称必须唯一且可持久。  
  
 `dwFlags`  
 中与项关联的标志。 可以是这些值的组合：  
  
|“值”|含义|  
|-----------|-------------|  
|SCRIPTITEM_CODEONLY|指示已命名的项表示一个仅包含代码的对象，并且该宿主没有要与此仅限代码的对象关联的 `IUnknown`。 主机只有此对象的名称。 在面向对象的语言（如C++）中，此标志将创建一个类。 并非所有语言都支持此标志。|  
|SCRIPTITEM_GLOBALMEMBERS|指示项是与脚本关联的全局属性和方法的集合。 通常，脚本引擎将忽略对象名称（而不是将其用作[IActiveScriptSite：： GetItemInfo](../../winscript/reference/iactivescriptsite-getiteminfo.md)方法的 cookie，或用于解析显式范围），并将其成员公开为全局变量和方法。 这使宿主可以扩展可供脚本使用的库（运行时函数等）。 脚本引擎将处理名称冲突（例如，当两个 SCRIPTITEM_GLOBALMEMBERS 项具有相同名称的方法）时，尽管不应由于此情况而返回错误。|  
|SCRIPTITEM_ISPERSISTENT|指示在保存脚本引擎时应保存项。 同样，如果设置此标志，则表示转换回已初始化状态应保留项的名称和类型信息（但脚本引擎必须释放指向实际对象上的接口的所有指针）。|  
|SCRIPTITEM_ISSOURCE|指示该脚本可以接收的项源事件。 子对象（自身对象中对象的属性）也可以将事件源到脚本。 这并不是递归的，但它为常见情况（例如创建容器及其所有成员控件）提供了一种方便的机制。|  
|SCRIPTITEM_ISVISIBLE|指示项的名称在脚本的命名空间中可用，并允许访问项的属性、方法和事件。 按照约定，项的属性包括项的子项;因此，所有子对象属性和方法（及其子级递归）都可访问。|  
|SCRIPTITEM_NOCODE|指示该项只是要添加到脚本的命名空间中的名称，不应被视为应该与代码关联的项。 例如，如果未设置此标志，则 VBScript 将为指定的项创建一个单独的模块， C++并可能为已命名的项创建单独的包装类。|  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|成功。|  
|`E_INVALIDARG`|参数无效。|  
|`E_POINTER`|指定的指针无效。|  
|`E_UNEXPECTED`|不应进行调用（例如，尚未加载或初始化脚本引擎）。|  
  
## <a name="see-also"></a>请参阅  
 [IActiveScript](../../winscript/reference/iactivescript.md)