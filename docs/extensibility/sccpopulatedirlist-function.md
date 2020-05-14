---
title: 放大缩小字体功能 放大缩小字体功能微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccPopulateDirList
helpviewer_keywords:
- SccPopulateDirList function
ms.assetid: dfff634b-b155-498b-a356-6eb252ac4fad
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4ac1c51ac694acadd2efb0cd7d1c5a3f1d66ebc1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700552"
---
# <a name="sccpopulatedirlist-function"></a>SccPopulateDirList 函数
此函数确定哪些目录和（可选）文件存储在源代码管理中，给定要检查的目录列表。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccPopulateDirList(
   LPVOID        pContext,
   LONG          nDirs,
   LPCSTR*       lpDirPaths,
   POPDIRLISTFUNCpfnPopulate,
   LPVOID        pvCallerData,
   LONG          fOptions
);
```

#### <a name="parameters"></a>参数
 pContext

[在]源代码管理插件上下文指针。

 nDirs

[在]`lpDirPaths`数组中的目录路径数。

 lpDirPath

[在]要检查的目录路径数组。

 pfn 填充

[在]回调函数用于调用中`lpDirPaths`每个目录路径和（可选）文件名（有关详细信息，请参阅[POPDIRLISTFUNC）。](../extensibility/popdirlistfunc.md)

 pvCallerData

[在]要传递给回调函数的值保持不变。

 fOptions

[在]控制目录处理方式的值的组合（请参阅[特定命令为可能的值使用的位标志的"](../extensibility/bitflags-used-by-specific-commands.md)填充 DirList 标志"部分）。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|已成功完成该操作”。|
|SCC_E_UNKNOWNERROR|出现了错误。|

## <a name="remarks"></a>备注
 只有实际上位于源代码管理存储库中的目录和（可选）文件名才会传递到回调函数。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [特定命令使用的位标志](../extensibility/bitflags-used-by-specific-commands.md)
- [POPDIRLISTFUNC](../extensibility/popdirlistfunc.md)
- [错误代码](../extensibility/error-codes.md)
