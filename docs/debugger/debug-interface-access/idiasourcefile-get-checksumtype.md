---
title: IDiaSourceFile::get_checksumType | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSourceFile::get_checksumType method
ms.assetid: 4c363e61-a6a9-409a-9cc0-d06eb2bee645
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c85c6ce8f03534c3ed810e530dbd12d8c6d115be
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72741832"
---
# <a name="idiasourcefileget_checksumtype"></a>IDiaSourceFile::get_checksumType
检索校验和类型。

## <a name="syntax"></a>语法

```C++
HRESULT get_checksumType ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄返回校验和类型。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="remarks"></a>备注
 校验和类型是可以映射到校验和算法的值。 例如，标准 PDB 文件格式通常可以具有以下值之一：

|校验和类型|CryptoAPI 标签|描述|
|-------------------|---------------------|-----------------|
|0|\<none>|不存在任何校验和。|
|1|`CALG_MD5`|用 MD5 哈希算法生成的校验和。|
|2|`CALG_SHA1`|用 SHA1 哈希算法生成的校验和。|

 @No__t_0 标签来自 `ALG_ID` 枚举。 有关哈希算法的详细信息，请参阅 Microsoft [!INCLUDE[winsdkshort](../../debugger/debug-interface-access/includes/winsdkshort_md.md)] 的 `CryptoAPI` 部分。

 若要获取源文件的实际校验和，请调用[IDiaSourceFile：： get_checksum](../../debugger/debug-interface-access/idiasourcefile-get-checksum.md)方法。

## <a name="see-also"></a>请参阅
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
- [IDiaSourceFile::get_checksum](../../debugger/debug-interface-access/idiasourcefile-get-checksum.md)