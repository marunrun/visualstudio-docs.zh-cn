---
title: IDiaSymbol::get_lexicalParentId | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_lexicalParentId method
ms.assetid: 6c0c2874-cc47-4e4f-ad9c-02a18a108d9d
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3d2d83a4ce3409096c188c24acf0e5d77d9689db
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840686"
---
# <a name="idiasymbolget_lexicalparentid"></a>IDiaSymbol::get_lexicalParentId
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

检索符号的词法父标识符。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT get_lexicalParentId (   
   DWORD* pRetVal  
);  
```  
  
#### <a name="parameters"></a>parameters  
 `pRetVal`  
 弄返回符号的词法父 ID。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回 `S_FALSE` 错误代码。  
  
> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。  
  
## <a name="remarks"></a>备注  
 标识符是由 DIA SDK 创建的唯一值，用于将所有符号标记为唯一。  
  
## <a name="see-also"></a>另请参阅  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
