---
title: 'Idialinenumber:: Get_statement |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaLineNumber::get_statement method
ms.assetid: 22b8ee29-79ef-427f-bd05-00d255ab836b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 397873a65176024327f371e9727b15984cd7d03f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62828385"
---
# <a name="idialinenumbergetstatement"></a>IDiaLineNumber::get_statement
检索一个标志，指示此行信息描述了一条语句，而不是程序源中的表达式的开头。

## <a name="syntax"></a>语法

```C++
HRESULT get_statement ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回`TRUE`如果此行信息描述程序源中的语句的开头。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果此属性不受支持。 否则，返回错误代码。

## <a name="remarks"></a>备注
 语句可以跨多个行。 此方法指示是否关联的行数表示的多行语句的开头。

## <a name="see-also"></a>请参阅
- [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)