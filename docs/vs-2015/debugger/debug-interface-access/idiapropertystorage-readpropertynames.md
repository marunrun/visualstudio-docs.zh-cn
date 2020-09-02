---
title: IDiaPropertyStorage：： ReadPropertyNames |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::ReadPropertyNames
ms.assetid: f8bcab77-afca-4a8f-8710-697842f8a518
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f3f6d3ac520a396b5207767a3fec0913c801c287
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62537350"
---
# <a name="idiapropertystoragereadpropertynames"></a>IDiaPropertyStorage::ReadPropertyNames
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索给定属性标识符对应的字符串名称。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT ReadPropertyNames (  
   ULONG         cpropid,  
   PROPID const* rgpropid,  
   BSTR*         rglpwstrName  
);  
```  
  
#### <a name="parameters"></a>参数  
 `cpropid`  
 中中属性 id 的数量 `rgpropid` 。  
  
 `rgpropid`  
 中要为其获取名称 (的属性 id 数组 `PROPID` 作为) 在 WTypes 中定义 `ULONG` 。  
  
 `rglpwstrName`  
 [in，out]指定的属性 id 的属性名称数组。 必须预先分配数组以容纳请求的属性名称数，并且必须能够至少保存 `cpropid``BSTR` 字符串。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="remarks"></a>备注  
 当不再需要函数时，必须通过调用函数) 来释放返回的属性名称 (`SysFreeString` 。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)
