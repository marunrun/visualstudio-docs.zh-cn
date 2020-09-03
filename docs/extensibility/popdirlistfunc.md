---
title: POPDIRLISTFUNC |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- POPLISTFUNC
helpviewer_keywords:
- POPDIRLISTFUNC callback function
ms.assetid: 0ee90fd2-5467-4154-ab4c-7eb02ac3a14c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 52a0c16af0e142bda8527c5244a22e0830ced9e0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80702082"
---
# <a name="popdirlistfunc"></a>POPDIRLISTFUNC
这是一个回调函数，该函数提供给 [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md) 函数以更新目录的集合，并 (可以选择性地) 文件名以找出受源代码管理的文件名称。

 `POPDIRLISTFUNC`只应为这些目录和文件名调用回调，此列表中 (`SccPopulateDirList` 是) 实际受源代码管理的函数。

## <a name="signature"></a>签名

```cpp
typedef BOOL (*POPDIRLISTFUNC)(
   LPVOID pvCallerData,
   BOOL bFolder,
   LPCSTR lpDirectoryOrFileName
);
```

## <a name="parameters"></a>参数
 pvCallerData

中向 [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md)提供的用户值。

 bFolder

[in] `TRUE` 如果中的名称 `lpDirectoryOrFileName` 是目录，则为; 否则为文件名。

 lpDirectoryOrFileName

中源代码管理下的目录或文件名的完整本地路径。

## <a name="return-value"></a>返回值
 IDE 将返回相应的错误代码：

|值|说明|
|-----------|-----------------|
|SCC_OK|继续处理。|
|SCC_I_OPERATIONCANCELED|停止处理。|
|SCC_E_xxx|任何适当的源代码管理错误都应停止处理。|

## <a name="remarks"></a>备注
 如果 `fOptions` 函数的参数 `SccPopulateDirList` 包含 `SCC_PDL_INCLUDEFILES` 标志，则该列表可能包含文件名和目录名。

## <a name="see-also"></a>另请参阅
- [IDE 实现的回调函数](../extensibility/callback-functions-implemented-by-the-ide.md)
- [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md)
- [错误代码](../extensibility/error-codes.md)
