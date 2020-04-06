---
title: 波普迪利斯芬奇 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702082"
---
# <a name="popdirlistfunc"></a>POPDIRLISTFUNC
这是为[SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md)函数提供的回调函数，用于更新目录和（可选）文件名的集合，以找出受源代码管理。

 `POPDIRLISTFUNC`应仅对实际受源代码管理的目录和文件名（在提供给`SccPopulateDirList`函数的列表中）调用回调。

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

[在]提供给[SccpopulateDirlist 的用户](../extensibility/sccpopulatedirlist-function.md)值 。

 bFolder

[在]`TRUE`如果 中`lpDirectoryOrFileName`的名称是目录;如果否则，名称是文件名。

 lpDirectoryOr文件名

[在]目录或文件名的完整本地路径，由源代码控制。

## <a name="return-value"></a>返回值
 IDE 返回相应的错误代码：

|值|说明|
|-----------|-----------------|
|SCC_OK|继续处理。|
|SCC_I_OPERATIONCANCELED|停止处理。|
|SCC_E_xxx|任何适当的源代码管理错误都应停止处理。|

## <a name="remarks"></a>备注
 如果`fOptions``SccPopulateDirList`函数的参数包含`SCC_PDL_INCLUDEFILES`标志，则列表可能包含文件名和目录名。

## <a name="see-also"></a>请参阅
- [IDE 实现的回调功能](../extensibility/callback-functions-implemented-by-the-ide.md)
- [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md)
- [错误代码](../extensibility/error-codes.md)
