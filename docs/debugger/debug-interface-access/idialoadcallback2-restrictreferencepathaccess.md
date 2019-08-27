---
title: IDiaLoadCallback2::RestrictReferencePathAccess | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback2::RestrictReferencePathAccess method
ms.assetid: e20cb45c-0360-4ff0-a92c-b1b6f76d6e85
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a39186cfc8fb3f83986692ebf7c608b895aae7ef
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62839727"
---
# <a name="idialoadcallback2restrictreferencepathaccess"></a>IDiaLoadCallback2::RestrictReferencePathAccess
确定是否在.exe 文件所在位置的路径中允许查找.pdb 文件。

## <a name="syntax"></a>语法

```C++
HRESULT RestrictReferencePathAccess();
```

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 以外的任何返回代码`S_OK`以免查找.exe 文件所在位置的.pdb 文件的路径中。

## <a name="see-also"></a>请参阅
- [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)