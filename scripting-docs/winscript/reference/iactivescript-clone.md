---
title: IActiveScript：： Clone |Microsoft Docs
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
ms.openlocfilehash: fbaad29cb31af26a0f26a1c679a900192fc77041
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72575800"
---
# <a name="iactivescriptclone"></a>IActiveScript::Clone
克隆当前脚本引擎（减去任何当前执行状态），并返回在当前线程中没有站点的加载的脚本引擎。 如果将其转换回已初始化状态，则此新脚本引擎的属性将与原始脚本引擎的属性相同。  
  
## <a name="syntax"></a>语法  
  
```cpp
HRESULT Clone(  
    IActiveScript **ppscript  // receives pointer to IActiveScript  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppscript`  
 弄变量的地址，该变量接收指向克隆的脚本引擎的[IActiveScript](../../winscript/reference/iactivescript.md)接口的指针。 宿主必须创建一个站点，并对新的脚本引擎调用[IActiveScript：： SetScriptSite](../../winscript/reference/iactivescript-setscriptsite.md)方法，然后它才会处于已初始化状态，因此可供使用。  
  
## <a name="return-value"></a>返回值  
 返回以下值之一：  
  
|返回值|含义|  
|------------------|-------------|  
|`S_OK`|成功。|  
|`E_NOTIMPL`|不支持此方法。|  
|`E_POINTER`|指定的指针无效。|  
|`E_UNEXPECTED`|不应进行调用（例如，尚未加载或初始化脚本引擎）。|  
  
## <a name="remarks"></a>备注  
 @No__t_0 方法是对 `IPersist*::Save`、`CoCreateInstance` 和 `IPersist*::Load` 的优化，因此新脚本引擎的状态应与原始脚本引擎的状态保存并加载到新的脚本引擎中的状态相同。 已命名的项在克隆的脚本引擎中重复，但会忘记每个项的特定对象指针，并通过[IActiveScriptSite：： GetItemInfo](../../winscript/reference/iactivescriptsite-getiteminfo.md)方法获取。 这允许使用与每个线程的入口点（单元模型）相同的对象模型。  
  
 此方法用于可运行同一脚本的多个实例的多线程服务器主机。 脚本引擎可能返回 `E_NOTIMPL`，在这种情况下，宿主可以通过复制持久状态并使用 `IPersist*` 接口创建脚本引擎的新实例来实现相同的结果。  
  
 此方法可从非基线程调用，而不会导致非基本标注宿主对象或[IActiveScriptSite](../../winscript/reference/iactivescriptsite.md)接口。  
  
## <a name="see-also"></a>请参阅  
 [IActiveScript](../../winscript/reference/iactivescript.md)