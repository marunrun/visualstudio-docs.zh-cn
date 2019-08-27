---
title: IDiaLoadCallback2::RestrictSystemRootAccess | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback2::RestrictSystemRootAccess method
ms.assetid: 39f22db8-632a-4ef0-babc-23f758e6d937
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 421581520f28037bc4b8fce9d546eaffad557f75
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62839714"
---
# <a name="idialoadcallback2restrictsystemrootaccess"></a>IDiaLoadCallback2::RestrictSystemRootAccess
确定是否在系统根目录下允许搜索.pdb 文件。

## <a name="syntax"></a>语法

```C++
HRESULT RestrictSystemRootAccess();
```

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 以外的任何返回代码`S_OK`阻止搜索.pdb 文件系统根目录。

## <a name="see-also"></a>请参阅
- [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)