---
title: 在检测中排除或包括短函数
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- profiling tools, instrument events
- profiling tools, include short functions
- profiling tools, exclude short functions
ms.assetid: eaeead79-aafe-4490-86ff-6ed4cad9c15f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b8f9601a39e755c1a3886f7049abd592d793fb4b
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/28/2019
ms.locfileid: "66261349"
---
# <a name="how-to-exclude-or-include-short-functions-from-instrumentation"></a>如何：在检测中排除或包括短函数
默认情况下，分析工具会从检测中排除*小型函数*。 小型函数是不执行任何函数调用的短函数。 排除这些小型函数会减少检测开销，从而提高检测速度。 排除小型函数还能减少性能分析数据文件 (.vsp) 的大小和分析所需的时间。 如果排除小型函数，花费在小型函数上的时间会减少，从而减少其父函数的独占和非独占时间。 可以在检测中排除或包括小型函数，具体在以下过程中说明。

### <a name="to-exclude-or-include-short-functions-from-instrumentation"></a>在检测中排除或包括短函数

1. 在“性能资源管理器”中，选择“性能会话”，然后右键单击并选择“属性”。

     随即显示“属性页”对话框。

2. 在“属性页”中，单击“检测”属性。

3. 若要从检测中排除短函数，请选择“从检测中排除短函数”。 此为默认设置。

     或

     若要在检测中包括短函数，请清除“从检测中排除短函数”。

4. 单击 **“确定”**。

## <a name="see-also"></a>请参阅
- [控制数据收集](../profiling/controlling-data-collection.md)
- [性能会话属性](../profiling/performance-session-properties.md)