---
title: SccBackgroundGet 函数 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80701234"
---
# <a name="sccbackgroundget-function"></a>SccBackgroundGet 函数
此函数从源控件中检索每个指定的文件，而无用户交互。

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

中源代码管理插件上下文指针。

 n

中数组中指定的文件数 `lpFileNames` 。

 lpFileNames

[in，out]要检索的文件的名称数组。

> [!NOTE]
> 名称必须为完全限定的本地文件名。

 dwFlags 

中命令标志 (`SCC_GET_ALL` ， `SCC_GET_RECURSIVE`) 。

 dwBackgroundOperationID

中与此操作关联的唯一值。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|操作已成功完成。|
|SCC_E_BACKGROUNDGETINPROGRESS|正在进行后台检索 (仅当源代码管理插件不支持) 同时运行批处理操作时，才应返回此项。|
|SCC_I_OPERATIONCANCELED|操作在完成前被取消。|

## <a name="remarks"></a>备注
 始终在与加载源代码管理插件的线程不同的线程上调用此函数。 在完成此函数之前，不应返回此函数;但是，可以在多个文件列表中对其进行多次调用，同时所有这些文件都是相同的。

 参数的使用与 `dwFlags` [SccGet](../extensibility/sccget-function.md)相同。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [SccGet](../extensibility/sccget-function.md)
