---
title: 使用率导航器 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.cv.performance.utilizationnavigator
ms.assetid: 522a981a-37ef-4cdd-a04c-f1e7525a2aab
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f4aec8cc1a707535e9cf6ae204be0a7ff67ea51d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68145333"
---
# <a name="utilization-navigator"></a>使用率导航器
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以使用并发可视化工具中的使用率导航器来选择跟踪中的时间间隔。 并发可视化工具显示目标进程在一段时间内的 CPU 内核使用率。 这样便于检查 CPU 使用率模式，还可以将使用率数据与其他视图中的数据进行比较。 使用率导航器显示在并发可视化工具的每个视图的顶部。 下图演示使用率导航器。  
  
 ![显示选定时间范围的利用率导航器](../profiling/media/cvutilizationnavigator.png "CVUtilizationNavigator")  
使用率导航器和选定的时间范围  
  
 在图中，选定的间隔由一个红色矩形来定义，称为 *thumb*。  
  
 此处演示如何通过使用率导航器来操作所显示的时间范围：  
  
- 可以通过左右拖动 Thumb 控件进行平移。 （键盘：将焦点移动到滚动块，然后按向左或向右键。）  
  
- 通过拖动其中一个图柄，可以更改间隔的程度。 （键盘：将焦点移动到图柄，然后按向右或向左键。）  
  
  如果使用另一种并发可视化工具缩放控件来更改间隔，则使用率导航器将会更新，以便反映所做的更改。
