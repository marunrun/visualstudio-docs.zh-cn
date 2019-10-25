---
title: IDiaDataSource：： openSession |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaDataSource::openSession method
ms.assetid: a3319ed0-3979-483b-9852-c0af96852c48
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7dd6ab61db3e3bafd594298aa41d32bce64d4941
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72744921"
---
# <a name="idiadatasourceopensession"></a>IDiaDataSource::openSession
为查询符号打开一个会话。

## <a name="syntax"></a>语法

```C++
HRESULT openSession ( 
   IDiaSession** ppSession
);
```

#### <a name="parameters"></a>参数
ppSession

弄返回表示打开的会话的[IDiaSession](../../debugger/debug-interface-access/idiasession.md)对象。

## <a name="return-value"></a>返回值
如果成功，将返回 `S_OK`;否则，将返回错误代码。 下表显示了此方法的可能的返回值。

|“值”|描述|
|-----------|-----------------|
|E_UNEXPECTED|尚未使用符号的源初始化[IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)对象。|
|E_INVALIDARG|`ppSession` 参数无效。|
|E_OUTOFMEMORY|没有足够的内存来打开会话。|

## <a name="remarks"></a>备注
此方法将为数据源打开一个[IDiaSession](../../debugger/debug-interface-access/idiasession.md)对象。

`IDiaSession` 对象将查询实现到数据源。 会话为每组调试符号管理一个地址空间。 如果数据源符号描述的 .exe 或 .dll 文件在多个地址范围内处于活动状态（例如，因为多个进程已加载了多个进程），则应使用每个地址范围的一个会话。

## <a name="example"></a>示例

```C++
IDiaSession* pSession;
HRESULT hr = pSource->openSession( &pSession );
if (FAILED(hr))
{
   // report error
}
```

## <a name="see-also"></a>请参阅
- [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)
- [概述](../../debugger/debug-interface-access/overview-debug-interface-access-sdk.md)
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [查询 .Pdb 文件](../../debugger/debug-interface-access/querying-the-dot-pdb-file.md)
