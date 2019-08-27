---
title: 如何：重新指定检测后的二进制文件的位置 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.property.binaries
helpviewer_keywords:
- binaries, instrumented
- instrumentation, instrumented binaries
- instrumented binaries and relocating
- profiling tools, instrumented binaries
ms.assetid: 258f49e8-4b09-477e-a132-8fad685b66f4
caps.latest.revision: 23
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 00b39b91b0a776438199d1df3c212cb9fe40f338
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68155518"
---
# <a name="how-to-relocate-instrumented-binaries"></a>如何：重定位已检测的二进制文件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在检测期间，探测器将插入二进制文件来评估应用程序性能。 通过选择重定位已检测的二进制文件，将检测原始二进制文件的副本，并将其放在指定位置。 如果不想要探查器重命名原始的二进制文件，可以选择此选项。 如果没有重定位该二进制文件，则将覆盖该二进制文件的原始版本。  
  
 **要求**  
  
- [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)], [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)], [!INCLUDE[vsPro](../includes/vspro-md.md)]  
  
### <a name="to-relocate-instrumented-binary"></a>若要重定位已检测的二进制文件  
  
1. 在“性能资源管理器”  中，右键单击性能会话，然后单击“属性”  。  
  
2. 在“属性页”  中，单击“二进制”  属性。  
  
3. 选择“重定位已检测的二进制文件”  复选框。  
  
4. 为已检测的二进制文件指定位置。  
  
## <a name="see-also"></a>请参阅  
 [配置性能会话](../profiling/configuring-performance-sessions.md)   
 [VSInstr](../profiling/vsinstr.md)
