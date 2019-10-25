---
title: IDiaEnumStackFrames | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumStackFrames interface
ms.assetid: 3d1e8403-c9fc-42ff-ae35-0ab9a5ed2ad7
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 83e6adb3157b67b89ef2c05f59eaaf2c7084d9d8
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72744006"
---
# <a name="idiaenumstackframes"></a>IDiaEnumStackFrames
枚举可用的各种堆栈帧。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法

|方法|描述|
|------------|-----------------|
|[IDiaEnumStackFrames::Next](../../debugger/debug-interface-access/idiaenumstackframes-next.md)|检索枚举序列中指定数目的堆栈帧元素。|
|[IDiaEnumStackFrames::Reset](../../debugger/debug-interface-access/idiaenumstackframes-reset.md)|将枚举序列重置到开始处。|

## <a name="remarks"></a>备注

## <a name="notes-for-callers"></a>调用方说明
通过调用[IDiaStackWalker：： getEnumFrames](../../debugger/debug-interface-access/idiastackwalker-getenumframes.md)或[IDiaStackWalker：： getEnumFrames2](../../debugger/debug-interface-access/idiastackwalker-getenumframes2.md)方法获取此接口。

## <a name="example"></a>示例
此示例演示如何获取和使用 `IDiaEnumStackFrames` 接口。 有关 `PrintStackFrame` 函数的实现，请参阅[IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)接口。

```C++
void DumpStackFrames(IDiaStackWalker*     pStackWalker,
                     IDiaStackWalkHelper* pStackWalkHelper,
                     CV_CPU_TYPE_e        cpuType)
{
    if (pStackWalker != NULL && pStackWalkHelper != NULL)
    {
        CComPtr<IDiaEnumStackFrames> pEnumsFrames;
        HRESULT hr;
        hr = pStackWalker->getEnumFrames2(cpuType, pStackWalkHelper, &pEnumFrames);
        if (SUCCEEDED(hr) && pEnumFrames != NULL)
        {
            CComPtr<IDiaStackFrame> pStackFrame;
            DWORD celt = 0;

            while (pEnumFrames->Next(1, &pStackFrame, &celt) == S_OK)
            {
                PrintStackFrame(pStackFrame);
            }
            pStackFrame = NULL;
        }
    }
}
```

## <a name="requirements"></a>要求
标头： Dia2

库： diaguids

DLL： msdia80

## <a name="see-also"></a>请参阅
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)
- [IDiaStackWalker::getEnumFrames2](../../debugger/debug-interface-access/idiastackwalker-getenumframes2.md)
- [IDiaStackWalker::getEnumFrames](../../debugger/debug-interface-access/idiastackwalker-getenumframes.md)
