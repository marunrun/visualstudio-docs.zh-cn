---
title: 消息标记 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.cv.markers.message
ms.assetid: 721f40ca-5af2-4a01-b8b6-2b90f6cb7f89
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 84c7a173bf0b7f5b3dc2187c0c8574819b2317a9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68176907"
---
# <a name="message-markers"></a>消息标记
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

消息标记代表日志输出。 消息是特定线程在特定时间发出的字符串。 可以将消息导出到文本文件，以便与其他工具一起使用。 可以将鼠标指针放在并发可视化工具中的某一消息上，以便查看消息字符串。 您可以在 [标记报告](../profiling/markers-report.md)中查看所有消息标记。  下图显示消息标记。  
  
## <a name="message-aggregation-markers"></a>消息聚合标记  
 有时，并发可视化工具中多个消息的发生时间过于接近，导致无法单独绘制。 发生这种情况时，将显示代表基础消息的消息聚合标记  。 当将鼠标指针放在这些图标上时，工具提示将显示所代表的基础消息数量。 若要查看这些消息，请放大。  如果一直放大但仍显示聚合标记，则可在[标记报告](../profiling/markers-report.md)中查看基础消息。  
  
## <a name="see-also"></a>另请参阅  
 [并发可视化工具标记](../profiling/concurrency-visualizer-markers.md)   
 [并发可视化工具 SDK](../profiling/concurrency-visualizer-sdk.md)
