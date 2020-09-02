---
title: SccUninitialize 函数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccUninitialize
helpviewer_keywords:
- SccUninitialize function
ms.assetid: 17cf5337-d251-4422-bc96-93fe7d48f2ae
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c4706ddf28949af4fe1bba01c32b2c64c9156d51
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80700228"
---
# <a name="sccuninitialize-function"></a>SccUninitialize 函数
此函数将清除之前对 [SccInitialize](../extensibility/sccinitialize-function.md) 的调用创建的任何分配或打开的连接，以便准备关闭源代码管理插件。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccUninitialize (
   LPVOID pvContext
);
```

#### <a name="parameters"></a>参数
 pvContext

中指向在 [SccInitialize](../extensibility/sccinitialize-function.md)中创建的源代码管理插件上下文结构的指针。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|清除已成功完成。|

## <a name="remarks"></a>备注
 源代码管理插件负责准备关闭并释放该插件已为上下文结构分配的内存的内存。 对于插件的每个给定实例，都将调用该函数一次。 在此调用之前调用 [SccInitialize](../extensibility/sccinitialize-function.md) 。 调用时，仍不能打开任何项目 `SccUninitialize` 。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
