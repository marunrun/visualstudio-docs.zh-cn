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
ms.openlocfilehash: 0ae024f0d91c980fa8e787b21c93d32a6431203e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62895839"
---
# <a name="endcapture"></a>EndCapture
结束以 `BeginCapture` 开始的捕获时间间隔。

## <a name="syntax"></a>语法

```C++
void EndCapture();
```

## <a name="remarks"></a>备注
 捕获时间间隔通常跨越一个帧的子集，例如，当您仅需要捕获有关某种绘图调用的图形信息时。 如果捕获时间间隔跨越对 present 的调用，则将捕获图形信息的两个帧。 第一个帧跨越对 `BeginCapture` 的调用与对 present 的调用之间的时间间隔；第二个帧跨越对 present 调用后的第一个 Direct3D 和对 `EndCapture` 调用之间的时间间隔。

 若要捕获时间间隔，您必须准备应用以捕获并记录图形信息-也就是说，您必须已调用[Init](init.md)的实例通过`VsgDbg`类，然后调用`BeginCapture`或`EndCapture`。

## <a name="see-also"></a>请参阅
- [BeginCapture](begincapture.md)
- [CaptureCurrentFrame](capturecurrentframe.md)