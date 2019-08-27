---
title: 降噪百分比 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.filter
helpviewer_keywords:
- Concurrency Visualizer, Noise Reduction Percentage
ms.assetid: 1c10cd4c-2fdd-48c9-b562-a334b3b2df6c
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c6407b40f58c3acc02705379768085793a2b79b6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68195557"
---
# <a name="noise-reduction-percentage"></a>降噪百分比
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

默认情况下，降噪百分比设置的值为 2。 调用树中只显示非独占时间百分比大于或等于此设置的项。 通过更改此设置，可以控制在调用树中显示的项数。 例如，如果将此值更改为 10，将只显示非独占时间百分比大于或等于 10% 的调用树项。 通过增大此设置的值，可以关注对进程性能影响较大的项。
