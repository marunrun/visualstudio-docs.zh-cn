---
title: 内存和分页性能规则 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: f37972b2-efe4-4a1c-a5d1-a246ccd76817
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5cc67d9b39bbcb3b55c593e26e85048d7c624fc8
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62421871"
---
# <a name="memory-and-paging-performance-rules"></a>内存和分页性能规则
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

内存和分页类别中的性能规则确定在分析运行期间能影响应用程序性能和响应能力的分页活动。  
  
|||  
|-|-|  
|[DA0014：以分页方式将活动内存移到磁盘的发生率极高](../profiling/da0014-extremely-high-rates-of-paging-active-memory-to-disk.md)|在整个分析运行期间出现了超高比率的分页活动内存进出磁盘的情况。 此级别的分页速率通常会影响应用程序性能和响应能力。 请考虑通过修改算法来减少内存分配。 可能还需要考虑应用程序的内存要求。 尝试在拥有更多内存的计算机上重新运行分析。 当分页活动数超过规则 D0017 的上限阈值时，将引发此规则。|  
|[DA0017：以分页方式将活动内存移到磁盘的发生率高](../profiling/da0017-high-rates-of-paging-active-memory-to-disk.md)|在整个分析运行期间出现了相对高比率的分页活动内存进出磁盘的情况。 此级别的分页速率通常会影响应用程序性能和响应能力。 请考虑通过修改算法来减少内存分配。 可能还需要考虑应用程序的内存要求。 尝试在拥有更多内存的计算机上重新运行分析。|
