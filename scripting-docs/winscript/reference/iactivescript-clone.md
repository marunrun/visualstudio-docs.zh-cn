---
title: IActiveScript::Clone | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScript.Clone
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScript_Clone
ms.assetid: aa000b2a-7085-448d-a422-f7adac7851cb
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: bec912596c792a67f65434062bc0d0ed11bd3fb9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62935700"
---
# <a name="iactivescriptclone"></a>IActiveScript::Clone
克隆当前脚本引擎 （减去任何当前执行状态），返回当前线程中没有站点加载脚本引擎。 此新的脚本引擎的属性将与原始脚本引擎会采用如果它已转换回为初始化状态的属性相同。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Clone(  
    IActiveScript **ppscript  // receives pointer to IActiveScript  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppscript`  
 [out]接收指向的变量的地址[IActiveScript](../../winscript/reference/iactivescript.md)克隆脚本引擎的接口。 主机必须创建一个站点，然后调用[iactivescript:: Setscriptsite](../../winscript/reference/iactivescript-setscriptsite.md)上新的脚本引擎之前它将处于初始化状态的方法，因此，可使用。  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|成功。|  
|`E_NOTIMPL`|不支持此方法。|  
|`E_POINTER`|指定了无效的指针。|  
|`E_UNEXPECTED`|不应在调用 （例如，脚本引擎具有尚未加载或初始化）。|  
  
## <a name="remarks"></a>备注  
 `IActiveScript::Clone`方法是一种优化方式的`IPersist*::Save`， `CoCreateInstance`，和`IPersist*::Load`，因此，像原始脚本引擎的状态已保存和加载到新的脚本引擎的新的脚本引擎状态应相同。 命名的项会有重复在克隆的脚本引擎中，但每个项的特定对象指针会忘记和所获得的采用[iactivescriptsite:: Getiteminfo](../../winscript/reference/iactivescriptsite-getiteminfo.md)方法。 这允许与每个线程入口点 （单元模型） 要使用的相同对象模型。  
  
 此方法用于可以运行同一个脚本的多个实例的多线程的服务器主机。 脚本引擎可能会返回`E_NOTIMPL`，在这种情况下，主机可以通过复制的持久状态并创建与脚本引擎的新实例实现相同的结果`IPersist*`接口。  
  
 此方法可以从非基础线程调用不会导致到主机对象或一个非基本标注[IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)接口。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScript](../../winscript/reference/iactivescript.md)