---
title: IDiaEnumSectionContribs：： Clone |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSectionContribs::Clone method
ms.assetid: 81d3f3a7-3684-4e5c-b028-29b268684a2c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ad6a561308999092344fe4c20038ec2cb78a86f4
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72744328"
---
# <a name="idiaenumsectioncontribsclone"></a>IDiaEnumSectionContribs::Clone
创建与当前枚举数包含相同枚举状态的枚举数。

## <a name="syntax"></a>语法

```C++
HRESULT Clone( 
   IDiaEnumSectionContrib** ppenum
);
```

#### <a name="parameters"></a>参数
 ppenum

弄返回一个[IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md)对象，该对象包含枚举器的副本。 部分发布不是重复的，只是枚举器。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md)