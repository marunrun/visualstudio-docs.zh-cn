---
title: IDiaLoadCallback2::RestrictOriginalPathAccess | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback2::RestrictOriginalPathAccess method
ms.assetid: 31fde3af-2824-4b0f-8d0d-cee6046596f6
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 26539d4217682b4d5357f13e9f9368c81297da78
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62839740"
---
# <a name="idialoadcallback2restrictoriginalpathaccess"></a>IDiaLoadCallback2::RestrictOriginalPathAccess
确定是否可以在原始的调试目录中的.pdb 文件。

## <a name="syntax"></a>语法

```C++
HRESULT RestrictOriginalPathAccess ();
```

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 以外的任何返回代码`S_OK`可以防止查找原始的调试目录中的.pdb 文件。 原始的调试目录是编译为可执行文件时启用调试符号文件的路径。 此路径不一定是可执行文件所在的路径相同。

## <a name="see-also"></a>请参阅
- [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)