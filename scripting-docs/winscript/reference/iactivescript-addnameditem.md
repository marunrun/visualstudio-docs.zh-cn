---
title: IActiveScript::AddNamedItem | Microsoft Docs
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
ms.openlocfilehash: db0a97c01d948a0c26850ebd1c3f47c6e3900614
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62935792"
---
# <a name="iactivescriptaddnameditem"></a>IActiveScript::AddNamedItem
将根级别项的名称添加到脚本引擎的命名空间。 根级别项是具有属性和方法、 事件源或这三者的对象。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT AddNamedItem(  
    LPCOLESTR pstrName,  // address of item name  
    DWORD dwFlags          // item flags  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pstrName`  
 [in]从脚本来查看包含的项名称的缓冲区的地址。 名称必须唯一且可持久化。  
  
 `dwFlags`  
 [in]与项关联的标志。 可以是这些值的组合：  
  
|“值”|含义|  
|-----------|-------------|  
|SCRIPTITEM_CODEONLY|指示命名的项表示仅限代码的对象，并且该主机不具有`IUnknown`要与此仅限代码的对象相关联。 主机仅具有此对象的名称。 例如面向对象语言中C++，此标志会创建一个类。 并非所有语言都支持此标志。|  
|SCRIPTITEM_GLOBALMEMBERS|指示该项全局属性和方法与脚本关联的集合。 通常情况下，脚本引擎会忽略对象名称 (不是为了将作为 cookie [iactivescriptsite:: Getiteminfo](../../winscript/reference/iactivescriptsite-getiteminfo.md)方法，或用于解析显式作用域)，并公开其成员作为全局变量和方法。 这样，要扩展的库 （运行时函数等） 可供脚本使用的主机。 它将保持对脚本引擎来处理名称冲突 （例如，当两个 SCRIPTITEM_GLOBALMEMBERS 项具有相同名称的方法），但由于这种情况下应不会返回错误。|  
|SCRIPTITEM_ISPERSISTENT|指示是否保存脚本引擎应保存该项。 同样，设置此标志指示转换为初始化状态应保留项的名称和类型信息 （脚本引擎必须但是，释放所有指向上实际对象的接口）。|  
|SCRIPTITEM_ISSOURCE|指示项引起该脚本可以接收器的事件。 子对象 （对象的属性是对象本身） 还可以获得的脚本的事件。 这不是递归的但它提供了方便机制最常见的情况下，例如，创建一个容器和其成员的所有控件。|  
|SCRIPTITEM_ISVISIBLE|指示项的名称在脚本中，允许访问属性、 方法和事件的项的命名空间中可用。 按照约定的项的属性包括项的子级;因此，所有子对象属性和方法 （和其子项，以递归方式） 将是可访问。|  
|SCRIPTITEM_NOCODE|指示是只是要添加到脚本的命名空间名称的项，并且不被视为代码应为其关联的项。 例如，如果没有设置此标志，VBScript 将创建的命名项单独的模块和C++可能会创建已命名项目的单独的包装类。|  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|成功。|  
|`E_INVALIDARG`|参数无效。|  
|`E_POINTER`|指定了无效的指针。|  
|`E_UNEXPECTED`|不应在调用 （例如，脚本引擎具有尚未加载或初始化）。|  
  
## <a name="see-also"></a>请参阅  
 [IActiveScript](../../winscript/reference/iactivescript.md)