---
title: IDiaLoadCallback::RestrictRegistryAccess | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback::RestrictRegistryAccess method
ms.assetid: de4760c3-a746-4bab-8065-1388fed31b67
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 25e6397b65c717be65a9a707dd0a53fc70321acb
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62828501"
---
# <a name="idialoadcallbackrestrictregistryaccess"></a>IDiaLoadCallback::RestrictRegistryAccess
确定是否可以使用注册表查询来查找符号搜索路径。

## <a name="syntax"></a>语法

```C++
HRESULT RestrictRegistryAccess();
```

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 以外的任何返回代码`S_OK`可防止查询符号搜索路径的注册表。

## <a name="see-also"></a>请参阅
- [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)