---
title: 如何：重定位被检测二进制文件 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.property.binaries
helpviewer_keywords:
- binaries, instrumented
- instrumentation, instrumented binaries
- instrumented binaries and relocating
- profiling tools, instrumented binaries
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: cddbb0b3e27b841441937b7256ea32d722e25f5e
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "74774895"
---
# <a name="how-to-relocate-instrumented-binaries"></a>如何：重新指定检测后的二进制文件的位置

在检测期间，探测器将插入二进制文件来评估应用程序性能。 通过选择重定位已检测的二进制文件，将检测原始二进制文件的副本，并将其放在指定位置。 如果不想要探查器重命名原始的二进制文件，可以选择此选项。 如果没有重定位该二进制文件，则将覆盖该二进制文件的原始版本。

## <a name="to-relocate-instrumented-binary"></a>若要重定位已检测的二进制文件

1. 在“性能资源管理器”  中，右键单击性能会话，然后单击“属性”  。

2. 在“属性页”  中，单击“二进制”  属性。

3. 选择“重定位已检测的二进制文件”  复选框。

4. 为已检测的二进制文件指定位置。

## <a name="see-also"></a>另请参阅

[配置性能会话](../profiling/configuring-performance-sessions.md)
[VSInstr](../profiling/vsinstr.md)
