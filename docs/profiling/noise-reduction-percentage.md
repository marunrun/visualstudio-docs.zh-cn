---
title: 降噪百分比 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.filter
helpviewer_keywords:
- Concurrency Visualizer, Noise Reduction Percentage
ms.assetid: 1c10cd4c-2fdd-48c9-b562-a334b3b2df6c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9d3021aef3f9a2e11849991327a6ef8783b62439
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "62794308"
---
# <a name="noise-reduction-percentage"></a>降噪百分比
默认情况下，降噪百分比设置的值为 2。 调用树中只显示非独占时间百分比大于或等于此设置的项。 通过更改此设置，可以控制在调用树中显示的项数。 例如，如果将此值更改为 10，将只显示非独占时间百分比大于或等于 10% 的调用树项。 通过增大此设置的值，可以关注对进程性能影响较大的项。