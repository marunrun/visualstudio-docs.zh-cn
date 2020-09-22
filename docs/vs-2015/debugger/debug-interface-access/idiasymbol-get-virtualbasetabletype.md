---
title: IDiaSymbol::get_virtualBaseTableType | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_virtualBaseTableType method
ms.assetid: e0581c4f-0343-49b5-9754-a48477460e9f
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ea59822ebc568e843433f28f6e9b23f4df96fdb2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840487"
---
# <a name="idiasymbolget_virtualbasetabletype"></a>IDiaSymbol::get_virtualBaseTableType
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索虚拟基表指针的类型。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_virtualBaseTableType(  
   IDiaSymbol *pRetVal  
};  
```  
  
#### <a name="parameters"></a>parameters  
  
|参数|说明|  
|---------------|-----------------|  
|`pRetVal`|弄返回一个 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) 对象，该对象指定基表的类型。|  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回 `S_FALSE` 错误代码。  
  
> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。  
  
## <a name="remarks"></a>备注  
 虚拟基表指针 (`vbtptr`) 是 [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] 从虚拟基类处理继承的 vtable 中的隐藏指针。 `vbtptr`可以具有不同的大小，具体取决于继承的类。  
  
 此方法返回 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) 对象，该对象可用于确定 vbtptr 的大小。  
  
## <a name="requirements"></a>要求  
  
|要求|说明|  
|-----------------|-----------------|  
|标头：|dia2|  
|版本：|DIA SDK v8.0|  
  
## <a name="see-also"></a>另请参阅  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
