---
title: UI 处理时间 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.uiprocessing
helpviewer_keywords:
- Concurrency Visualizer, UI Processing Time
ms.assetid: 0ddb05a3-8c6b-448b-8488-2751c1e5abcc
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 4bbed9d8c4725b6bd497377d4a9dee22f2f8573d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68145486"
---
# <a name="ui-processing-time"></a>UI 处理时间
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

时间线中的这些时间段与归类为 UI 处理的阻塞时间关联。 这表示有一个线程正在发送 Windows 消息或正在执行其他用户界面 (UI) 操作。 在此时间内，线程已在被并发可视化工具计数为 UI 处理的 API 中阻塞。 `GetMessage()` 和 `MsgWaitForMultipleObjects()` 等 API 就归为此组。  
  
 如果未标识预定义的阻塞 API，请检查调用堆栈和分析报告，确定造成延迟的根本原因。  
  
 UI 处理类别对于了解 GUI 应用程序的响应能力很重要，非常适合依赖 UI 响应能力的应用程序。 例如，如果应用程序中的 UI 线程能够将 100% 的时间用于 UI 处理，则该应用程序的响应速度可能会非常快。 但是，如果 UI 线程花费了大量时间在其他类别上，则需查找根本原因并考虑降低该线程上的非 UI 类别。  
  
## <a name="see-also"></a>另请参阅  
 [“线程”视图](../profiling/threads-view-parallel-performance.md)
