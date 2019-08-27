---
title: CaptureCurrentFrame | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 4509311d-6fe2-4b65-9b4a-ff0522585d6a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ec67013b41a5ec8876866044355534c42bfe2ee0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62848708"
---
# <a name="capturecurrentframe"></a>CaptureCurrentFrame
将当前帧的剩余部分捕获到图形日志文件。

## <a name="syntax"></a>语法

```C++
void CaptureCurrentFrame();
```

## <a name="remarks"></a>备注
 如果另一个捕获当前正在进行中（例如，通过 `BeginCapture` 函数启动的捕获），则将完成该捕获并将其记录到图形日志以作为不同的帧。 紧跟着，图形诊断开始捕获当前帧的剩余部分，此部分也记录为不同的帧。 通过调用 present 来标记当前帧的结尾。

 若要捕获帧，您必须准备应用以捕获并记录图形信息-也就是说，您必须具有名为[Init](init.md)的实例通过`VsgDbg`类，然后调用`CaptureCurrentFrame`。

## <a name="see-also"></a>请参阅
- [Init](init.md)
- [BeginCapture](begincapture.md)