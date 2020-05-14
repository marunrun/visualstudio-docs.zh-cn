---
title: 查询更改 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- QUERYCHANGESFUNC
helpviewer_keywords:
- QUERYCHANGESFUNC callback function
- QUERYCHANGESDATA structure
ms.assetid: 9d383e2c-eee1-4996-973a-0652d4c5951c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 30864cae95672f4026084a94c5474d165b124cba
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701633"
---
# <a name="querychangesfunc"></a>QUERYCHANGESFUNC
这是[SccQueryChanges](../extensibility/sccquerychanges-function.md)操作用于枚举文件名集合并确定每个文件状态的回调函数。

 该`SccQueryChanges`函数被赋予文件列表和指向回调的`QUERYCHANGESFUNC`指针。 源代码管理插件枚举给定列表，并为此列表中的每个文件提供状态（通过此回调）。

## <a name="signature"></a>签名

```cpp
typedef BOOL (*QUERYCHANGESFUNC)(
   LPVOID pvCallerData,
   QUERYCHANGESDATA * pChangesData
);
```

## <a name="parameters"></a>参数
 pvCallerData

[在]调用`pvCallerData`方 （IDE） 传递给[SccQuery 更改](../extensibility/sccquerychanges-function.md)的参数。 源代码管理插件不应对此值的内容进行假设。

 p 更改数据

[在]指向描述对文件的更改的[QUERYCHANGESDATA 结构结构](#LinkQUERYCHANGESDATA)的指针。

## <a name="return-value"></a>返回值
 IDE 返回相应的错误代码：

|值|说明|
|-----------|-----------------|
|SCC_OK|继续处理。|
|SCC_I_OPERATIONCANCELED|停止处理。|
|SCC_E_xxx|任何适当的 SCC 错误都应停止处理。|

## <a name="querychangesdata-structure"></a><a name="LinkQUERYCHANGESDATA"></a>查询更改数据结构
 为每个文件传入的结构如下所示：

```cpp
struct QUERYCHANGESDATA_A
{
    DWORD  dwSize;
    LPCSTR lpFileName;
    DWORD  dwChangeType;
    LPCSTR lpLatestName;
};

typedef struct QUERYCHANGESDATA_A QUERYCHANGESDATA;

struct QUERYCHANGESDATA_W
{
    DWORD   dwSize;
    LPCWSTR lpFileName;
    DWORD   dwChangeType;
    LPCWSTR lpLatestName;
};
```

 dwSize 此结构的大小（以字节为单位）。

 lpFile名称此项目的原始文件名。

 dwChangeType 代码指示文件的状态：

|代码|描述|
|----------|-----------------|
|`SCC_CHANGE_UNKNOWN`|无法判断发生了什么变化。|
|`SCC_CHANGE_UNCHANGED`|此文件没有名称更改。|
|`SCC_CHANGE_DIFFERENT`|具有不同标识的文件，但数据库中存在相同的名称。|
|`SCC_CHANGE_NONEXISTENT`|文件在数据库中或本地都不存在。|
|`SCC_CHANGE_DATABASE_DELETED`|在数据库中删除的文件。|
|`SCC_CHANGE_LOCAL_DELETED`|文件在本地删除，但该文件仍然存在于数据库中。 如果无法确定这一点，则`SCC_CHANGE_DATABASE_ADDED`返回 。|
|`SCC_CHANGE_DATABASE_ADDED`|文件添加到数据库，但本地不存在。|
|`SCC_CHANGE_LOCAL_ADDED`|文件在数据库中不存在，是一个新的本地文件。|
|`SCC_CHANGE_RENAMED_TO`|文件重命名或移动到数据库中为`lpLatestName`。|
|`SCC_CHANGE_RENAMED_FROM`|文件重命名或从`lpLatestName`中移动到数据库中。如果跟踪费用太高，则返回其他标志，如`SCC_CHANGE_DATABASE_ADDED`。|

 lpLatest名称此项目的当前文件名。

## <a name="see-also"></a>请参阅
- [IDE 实现的回调功能](../extensibility/callback-functions-implemented-by-the-ide.md)
- [SccQueryChanges](../extensibility/sccquerychanges-function.md)
- [错误代码](../extensibility/error-codes.md)
