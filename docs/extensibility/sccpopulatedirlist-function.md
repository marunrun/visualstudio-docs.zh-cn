---
title: SccPopulateDirList 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccPopulateDirList
helpviewer_keywords:
- SccPopulateDirList function
ms.assetid: dfff634b-b155-498b-a356-6eb252ac4fad
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f13c674e6374e826dc45343e5cd1f7edcc1f8100
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72720900"
---
# <a name="sccpopulatedirlist-function"></a>SccPopulateDirList 函数
此函数确定哪些目录和（可选）文件存储在源代码管理中，提供要检查的目录列表。

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

中@No__t_0 数组中目录路径的数目。

 lpDirPaths

中要检查的目录路径的数组。

 pfnPopulate

中为 `lpDirPaths` 中的每个目录路径和（可选）文件名调用的回调函数（有关详细信息，请参阅[POPDIRLISTFUNC](../extensibility/popdirlistfunc.md) ）。

 pvCallerData

中将以不更改的形式传递给回调函数的值。

 用于

中用于控制如何处理目录的值的组合（有关可能值，请参阅[特定命令使用的 Bitflags](../extensibility/bitflags-used-by-specific-commands.md)的 "PopulateDirList 标志" 部分）。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|“值”|描述|
|-----------|-----------------|
|SCC_OK|已成功完成操作。|
|SCC_E_UNKNOWNERROR|出现了错误。|

## <a name="remarks"></a>备注
 仅源控件存储库中实际的那些目录和（可选）文件名会传递到回调函数。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [特定命令使用的位标志](../extensibility/bitflags-used-by-specific-commands.md)
- [POPDIRLISTFUNC](../extensibility/popdirlistfunc.md)
- [错误代码](../extensibility/error-codes.md)