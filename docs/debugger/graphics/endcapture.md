---
title: EndCapture | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 06084c3b-e065-49b6-968e-d578762fb871
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c54e8b12f4d3b924b363f42cb098a1d528a8108b
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72735981"
---
# <a name="endcapture"></a>EndCapture
结束以 `BeginCapture` 开始的捕获时间间隔。

## <a name="syntax"></a>语法

```C++
void EndCapture();
```

## <a name="remarks"></a>备注
 捕获时间间隔通常跨越一个帧的子集，例如，当您仅需要捕获有关某种绘图调用的图形信息时。 如果捕获时间间隔跨越对 present 的调用，则将捕获图形信息的两个帧。 第一个帧跨越对 `BeginCapture` 的调用与对 present 的调用之间的时间间隔；第二个帧跨越对 present 调用后的第一个 Direct3D 和对 `EndCapture` 调用之间的时间间隔。

 若要捕获时间间隔，必须准备应用来捕获并记录图形信息 - 也就是说，必须先通过 `VsgDbg` 类的实例调用 [Init](init.md)，然后才能调用 `BeginCapture` 或 `EndCapture`。

## <a name="see-also"></a>请参阅
- [BeginCapture](begincapture.md)
- [CaptureCurrentFrame](capturecurrentframe.md)