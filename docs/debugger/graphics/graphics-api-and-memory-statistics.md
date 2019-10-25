---
title: 图形 API 和内存统计信息 |Microsoft Docs
ms.date: 03/02/2017
ms.topic: conceptual
f1_keywords:
- vs.graphics.apistatistics
- vs.graphics.memorystatistics
ms.assetid: 27d2f303-e3ed-4219-9009-345a0d849506
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fa808e76e6655c5d57108c923b19794d0398b80c
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72735576"
---
# <a name="graphics-api-and-memory-statistics"></a>图形 API 和内存统计信息
<!-- VERSIONLESS -->
Visual Studio 2017 和更高版本支持图形 API 统计信息和内存统计信息工具。  使用这两个工具可以查看有关 Direct3D API 使用情况的各种信息，以及各种资源的 GPU 内存消耗。

## <a name="graphics-api-statistics"></a>图形 API 统计信息
利用 Visual 图形诊断 Studio 中的图形 API 统计信息，你可以查看已进行的所有 Direct3D 调用，以及每个调用的计数。  若要查看窗口，请选择 "**查看 > API 统计信息**" 菜单项。

![API 统计信息](media/gfx_diag_api_statistics.png)

此工具可用于发现你可能未意识到的 DirectX 调用，或你过于频繁地进行调用。

您可以在窗口中右键单击以将所有数据复制为 CSV，然后将其粘贴到 Excel 之类的内容中进行进一步分析。

## <a name="memory-statistics"></a>内存统计信息
此工具将显示为帧中创建的资源分配图形驱动程序的内存量。  若要查看此窗口，请选择 "**查看 > 内存统计信息**" 菜单项。

![内存统计信息](media/gfx_diag_memory_statistics.png)

" **GPU 分配**" 列显示**事件**列中显示的事件所使用的内存量。  还可以选择 "监视" 图标 ![watch "图标 ](media/gfx_watch.png) 查看所选事件的[资源历史记录](graphics-event-list.md#resource-history)。

与 API 统计信息工具一样，你可以在窗口中右键单击以将所有数据复制为 CSV，这可以将其粘贴到 Excel 之类的内容中进行进一步分析。

## <a name="see-also"></a>请参阅
- [图形诊断（调试 DirectX 图形）](visual-studio-graphics-diagnostics.md)
- [资源历史记录](graphics-event-list.md#resource-history)
<!-- /VERSIONLESS -->