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
ms.openlocfilehash: 7810889d4af411477573c71aa694d797a90763f3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62896014"
---
# <a name="graphics-api-and-memory-statistics"></a>图形 API 和内存统计信息
<!-- VERSIONLESS -->
Visual Studio 2017 和更高版本支持的图形 API 统计信息和内存统计信息的工具。  这两种工具使您可以查看有关 Direct3D API 使用情况，以及各种资源的 GPU 内存消耗的各种信息的位。

## <a name="graphics-api-statistics"></a>图形 API 统计信息
Visual Studio 图形诊断中的图形 API 统计信息，可以查看所有所做的 Direct3D 调用和每个调用的计数。  若要查看窗口，请选择**视图 > API 统计信息**菜单项。

![API 统计信息](media/gfx_diag_api_statistics.png)

此工具可以轻松发现你可能没有意识到您的 DirectX 调用正在进行，或在经常进行的调用。

您可以右键单击在窗口中复制所有数据以 csv 格式，可以粘贴到类似于 Excel 的内容进行进一步分析。

## <a name="memory-statistics"></a>内存统计信息
此工具将显示在框架中创建图形驱动程序分配的资源的内存量。  若要查看此窗口，请选择**视图 > 内存统计信息**菜单项。

![内存统计信息](media/gfx_diag_memory_statistics.png)

**GPU 分配**列显示的事件中显示所用的内存量**事件**列。  此外可以选择监视图标![监视图标](media/gfx_watch.png)若要查看[资源历史记录](graphics-event-list.md#resource-history)所选事件。

与 API 统计信息工具，可以右键单击在窗口中复制所有数据以 csv 格式，可以粘贴到类似于 Excel 的内容进行进一步分析。

## <a name="see-also"></a>请参阅
- [图形诊断（调试 DirectX 图形）](visual-studio-graphics-diagnostics.md)
- [资源历史记录](graphics-event-list.md#resource-history)
<!-- /VERSIONLESS -->