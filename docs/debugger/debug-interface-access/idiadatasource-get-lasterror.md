---
title: IDiaDataSource：： get_lastError |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaDataSource::get_lastError method
ms.assetid: cf08850b-8b75-4e8c-90bd-bd0214756f99
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 48595dda70560f555533a1857f73db4d7bd20a86
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72744976"
---
# <a name="idiadatasourceget_lasterror"></a>IDiaDataSource::get_lastError
检索最后一个加载错误的文件名。

## <a name="syntax"></a>语法

```C++
HRESULT get_lastError (
   BSTR* pRetVal
);
```

#### <a name="parameters"></a>参数
 pRetVal

弄返回一个字符串，该字符串包含与上一次加载错误关联的 .pdb 文件名。

## <a name="return-value"></a>返回值
 返回由加载操作引起的最后一个错误代码。 如果 `pRetVal` 参数 `NULL`，则返回 `E_INVALIDARG`。

## <a name="example"></a>示例

```C++
BSTR    fileName;
HRESULT errorCode = pSource->get_lastError( &fileName );
```

## <a name="see-also"></a>请参阅
- [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)