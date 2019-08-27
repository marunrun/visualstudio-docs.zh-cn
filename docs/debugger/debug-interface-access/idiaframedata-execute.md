---
title: IDiaFrameData::execute | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::execute method
ms.assetid: 7a6c7d03-1ff1-4059-bd54-5f407eeebc26
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 78440c703ece2aa54e54594d57156dbb17848915
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62832646"
---
# <a name="idiaframedataexecute"></a>IDiaFrameData::execute
执行堆栈展开并在堆栈遍历帧界面中返回结果。

## <a name="syntax"></a>语法

```C++
HRESULT execute ( 
   IDiaStackWalkFrame* frame
);
```

#### <a name="parameters"></a>参数
 `frame`

[in][IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)保留帧寄存器状态的对象。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。 下表显示了可能的此方法的返回值。

|“值”|描述|
|-----------|-----------------|
|E_DIA_INPROLOG|无法执行序言代码中的堆栈帧。|
|E_DIA_SYNTAX|分析帧程序中遇到错误。|
|E_DIA_FRAME_ACCESS|无法访问寄存器或内存。|
|E_DIA_VALUE|计算某个值 （例如，被零除） 时出错。|

## <a name="remarks"></a>备注
 若要展开堆栈在调试期间调用此方法。 [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)对象由客户端应用程序接收到寄存器的更新，并为使用的方法实现`execute`方法。

## <a name="see-also"></a>请参阅
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
- [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)