---
title: StackFrameTypeEnum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- StackFrameTypeEnum enumeration
ms.assetid: 61e40163-eee0-4c1f-af47-cef3771bdc41
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 20b0c9dd106e5744a369ddaa6cb870788f7464d3
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72738557"
---
# <a name="stackframetypeenum"></a>StackFrameTypeEnum
指定堆栈帧类型。

## <a name="syntax"></a>语法

```C++
enum StackFrameTypeEnum {
    FrameTypeFPO,
    FrameTypeTrap,
    FrameTypeTSS,
    FrameTypeStandard,
    FrameTypeFrameData,
    FrameTypeUnknown = -1
};
```

## <a name="elements"></a>元素
省略 `FrameTypeFPO` 帧指针;可用的 FPO 信息。

`FrameTypeTrap` 内核捕获帧。

`FrameTypeTSS` 内核捕获帧。

`FrameTypeStandard` 标准 EBP 堆栈帧。

省略 `FrameTypeFrameData` 帧指针;提供框架数据信息。

`FrameTypeUnknown` 没有任何调试信息的帧。

## <a name="remarks"></a>备注
此枚举中的值由对[IDiaStackFrame：： get_type](../../debugger/debug-interface-access/idiastackframe-get-type.md)方法的调用返回。

## <a name="requirements"></a>要求
标头： cvconst

## <a name="see-also"></a>请参阅
- [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaStackFrame::get_type](../../debugger/debug-interface-access/idiastackframe-get-type.md)
