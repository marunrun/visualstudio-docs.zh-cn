---
title: Scc 解初始化功能 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700228"
---
# <a name="sccuninitialize-function"></a>SccUninitialize 函数
此功能清理以前调用[Scc初始化](../extensibility/sccinitialize-function.md)创建的任何分配或打开连接，以准备关闭源代码管理插件。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccUninitialize (
   LPVOID pvContext
);
```

#### <a name="parameters"></a>参数
 pvContext

[在]指向在[Scc 初始化](../extensibility/sccinitialize-function.md)中创建的源代码管理插件上下文结构的指针。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|清理工作成功完成。|

## <a name="remarks"></a>备注
 源代码管理插件负责准备关闭和释放插件为上下文结构分配的内存。 对于插件的每个给定实例，该函数调用一次。 在此调用之前，对[Scc 初始化的](../extensibility/sccinitialize-function.md)调用。 调用 时仍无法打开任何项目`SccUninitialize`。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
