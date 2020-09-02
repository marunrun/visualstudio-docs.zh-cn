---
title: SccPopulateDirList 函数 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80700552"
---
# <a name="sccpopulatedirlist-function"></a>SccPopulateDirList 函数
给定要检查的目录列表，此函数确定哪些目录和 (可) 选择将文件存储在源代码管理中。

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

中源代码管理插件上下文指针。

 nDirs

中数组中目录路径的数目 `lpDirPaths` 。

 lpDirPaths

中要检查的目录路径的数组。

 pfnPopulate

中为每个目录路径调用的回调函数，并 (可以选择在 (中) 文件名， `lpDirPaths` 请参阅 [POPDIRLISTFUNC](../extensibility/popdirlistfunc.md) 了解详细信息) 。

 pvCallerData

中将以不更改的形式传递给回调函数的值。

 用于

中用于控制如何处理目录的值的组合 (参见 [特定命令使用的 Bitflags](../extensibility/bitflags-used-by-specific-commands.md) 的 "PopulateDirList 标志" 部分，以查找可能的值) 。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|已成功完成该操作”。|
|SCC_E_UNKNOWNERROR|出现了错误。|

## <a name="remarks"></a>备注
 仅在源代码管理存储库中实际具有的这些目录和 (（可选）) 文件名称将传递给回调函数。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [特定命令使用的位标志](../extensibility/bitflags-used-by-specific-commands.md)
- [POPDIRLISTFUNC](../extensibility/popdirlistfunc.md)
- [错误代码](../extensibility/error-codes.md)
