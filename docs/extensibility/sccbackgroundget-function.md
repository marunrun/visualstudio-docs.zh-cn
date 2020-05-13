---
title: Scc背景获取功能 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccBackgroundGet
helpviewer_keywords:
- SccBackgroundGet function
ms.assetid: 69817e52-b9ac-4f4d-820b-2cc9c384f0dc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b1c07076b6e257bd5519d19f841797fbc652f0c1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701234"
---
# <a name="sccbackgroundget-function"></a>Scc背景获取功能
此函数从源代码管理检索每个指定的文件，而没有用户交互。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccBackgroundGet(
   LPVOID  pContext,
   LONG    nFiles,
   LPCSTR* lpFileNames,
   LONG    dwFlags,
   LONG    dwBackgroundOperationID
);
```

### <a name="parameters"></a>参数
 pContext

[在]源代码管理插件上下文指针。

 n文件

[在]`lpFileNames`数组中指定的文件数。

 lpFile名称

[进出]要检索的文件的名称数组。

> [!NOTE]
> 名称必须是完全限定的本地文件名。

 dwFlags

[在]命令标志`SCC_GET_ALL`（。 `SCC_GET_RECURSIVE`

 dw背景操作ID

[在]与此操作关联的唯一值。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|操作已成功完成。|
|SCC_E_BACKGROUNDGETINPROGRESS|后台检索已在进行中（源代码管理插件应仅当它不支持同时批处理操作时才返回它）。|
|SCC_I_OPERATIONCANCELED|操作在完成之前已取消。|

## <a name="remarks"></a>备注
 此函数始终调用与加载源代码管理插件不同的线程。 在完成之前，不应返回此功能;但是，它可以调用多个文件列表，同时调用。

 参数的使用`dwFlags`与[SccGet](../extensibility/sccget-function.md)相同。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 功能](../extensibility/source-control-plug-in-api-functions.md)
- [SccGet](../extensibility/sccget-function.md)
