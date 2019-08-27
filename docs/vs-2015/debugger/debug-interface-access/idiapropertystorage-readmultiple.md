---
title: IDiaPropertyStorage::ReadMultiple |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadMultiple
ms.assetid: 6ccc9397-ce41-4f72-b261-72ac252cd4a5
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 40cd84e00f2e6abea285368a6206c7400abf8877
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62538078"
---
# <a name="idiapropertystoragereadmultiple"></a>IDiaPropertyStorage::ReadMultiple
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

读取指定的属性从当前的属性集。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT ReadMultiple(   
   ULONG          cpspec,  
   PROPSPEC const rgpspec,  
   PROPVARIANT    rgvar  
);  
```  
  
#### <a name="parameters"></a>参数  
 `cpspec`  
 [in]属性中指定的计数`rgpspec`数组。 如果为零，则方法返回没有属性，但的确会返回`S_OK`作为成功代码。  
  
 `rgpspec`  
 [in]要读取的属性数组。 属性 ID 或可选的字符串名称，可以指定属性。 不需要在数组中任何特定顺序中指定属性。 该数组可以包含重复的属性，从而导致重复的属性值返回时的简单属性。 非简单属性应返回访问被拒绝在尝试再次将其打开。 数组可以包含的属性 Id 和字符串 Id 的组合。 此数组必须至少具有`cpspec`属性值的数目。  
  
 `rgvar`  
 [in、 out]一个数组`PROPVARIANT`结构 （Microsoft.VisualStudio.OLE.Interop 命名空间中） 若要使用的每个属性的值进行填充。 该数组必须至少是`cpspec`大小中的元素。 调用方不需要初始化数组中的值。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果未找到一个或多个属性。 否则，返回错误代码。  
  
## <a name="remarks"></a>备注  
 如果未找到属性中的相应条目`rgvar`数组包含`VARIANT`类型为`VT_EMPTY`。  
  
## <a name="see-also"></a>请参阅  
 [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)
