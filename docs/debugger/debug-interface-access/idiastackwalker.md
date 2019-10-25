---
title: IDiaStackWalker | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalker interface
ms.assetid: 4a61a22a-9cf8-4ea1-9e6e-b42f96872d40
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2366c933bf072c295b29d06ff5610bd3735c0077
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72741512"
---
# <a name="idiastackwalker"></a>IDiaStackWalker
提供使用 .pdb 文件中的信息执行堆栈审核的方法。

## <a name="syntax"></a>语法

```
IDiaStackWalker: IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
下表显示 `IDiaStackWalker` 的方法。

|方法|描述|
|------------|-----------------|
|[IDiaStackWalker::getEnumFrames](../../debugger/debug-interface-access/idiastackwalker-getenumframes.md)|检索 x86 平台的堆栈帧枚举器。|
|[IDiaStackWalker::getEnumFrames2](../../debugger/debug-interface-access/idiastackwalker-getenumframes2.md)|检索特定平台类型的堆栈帧枚举器。|

## <a name="remarks"></a>备注
此接口用于获取已加载模块的堆栈帧的列表。 每个方法都传递一个[IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)对象（由客户端应用程序实现），该对象提供创建堆栈帧列表所需的信息。

## <a name="notes-for-callers"></a>调用方说明
此接口是通过以下方法获取的：调用具有类标识符 `CLSID_DiaStackWalker` 的 `CoCreateInstance` 方法和 `IID_IDiaStackWalker` 的接口 ID。 该示例演示如何获取此接口。

## <a name="example"></a>示例
此示例演示如何获取 `IDiaStackWalker` 接口。

```C++

IDiaStackWalker* pStackWalker;
HRESULT hr = CoCreateInstance(CLSID_DiaStackWalker,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IDiaStackWalker,
                              (void**) &pStackWalker);
if (FAILED(hr))
{
    // Report error and exit
}
```

## <a name="requirements"></a>要求
标头： Dia2

库： diaguids

DLL： msdia80

## <a name="see-also"></a>请参阅
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
