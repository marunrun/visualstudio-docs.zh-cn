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
ms.openlocfilehash: 9a6508b8cfde2f08eb40201973fec899ee11956b
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353550"
---
# <a name="sccpopulatedirlist-function"></a>SccPopulateDirList 函数
此函数将确定哪些目录和 （可选） 文件存储在源代码管理，提供要检查的目录的列表。

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

[in]源控件插件上下文指针。

 nDirs

[in]中的目录路径数量`lpDirPaths`数组。

 lpDirPaths

[in]若要检查的目录路径的数组。

 pfnPopulate

[in]要为每个目录路径和 （可选） 中的文件名调用的回调函数`lpDirPaths`(请参阅[POPDIRLISTFUNC](../extensibility/popdirlistfunc.md)有关详细信息)。

 pvCallerData

[in]要传递的值保持不变的回调函数。

 fOptions

[in]控制处理目录的方式的值的组合 (请参阅的"PopulateDirList 标志"部分[位标志由特定命令](../extensibility/bitflags-used-by-specific-commands.md)有关可能的值)。

## <a name="return-value"></a>返回值
 此函数的源控制插件实现应返回以下值之一：

|值|描述|
|-----------|-----------------|
|SCC_OK|已成功完成操作。|
|SCC_E_UNKNOWNERROR|出现了错误。|

## <a name="remarks"></a>备注
 仅这些目录和 （可选） 实际上是在源控件存储库中的文件名称传递到回调函数。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [特定命令使用的位标志](../extensibility/bitflags-used-by-specific-commands.md)
- [POPDIRLISTFUNC](../extensibility/popdirlistfunc.md)
- [错误代码](../extensibility/error-codes.md)