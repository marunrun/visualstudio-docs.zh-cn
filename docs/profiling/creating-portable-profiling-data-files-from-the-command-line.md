---
title: 分析命令行 - 创建可移植的数据文件
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 2ceb63a7-b835-4988-b756-2afc3fcc4808
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: d0584cd2a476a7552beec483dd72ad1e957800ec
ms.sourcegitcommit: 566144d59c376474c09bbb55164c01d70f4b621c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2020
ms.locfileid: "90808833"
---
# <a name="create-portable-profiling-data-files-from-the-command-line"></a>从命令行创建可移植的分析数据文件
若要更轻松地共享分析数据，可以使用 [VSPerfReport](../profiling/vsperfreport.md) 命令行工具将用于分析运行的符号嵌入到 .vsp 文件中。

 还可以创建经过预先分析的分析数据 (.vsps) 文件，此文件较小，可在 IDE 中快速加载。

> [!NOTE]
> 请确保符号 (.pdb) 文件可供 VSPerfReport 使用。 有关详细信息，请参阅[如何：通过命令行指定符号文件位置](../profiling/how-to-specify-symbol-file-locations-from-the-command-line.md)。
>
> 有关 VSReport 路径的信息，请参阅[指定命令行工具的路径](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)。
>
> 无法筛选 .vsps 文件中的分析数据。

### <a name="to-embed-the-symbols-for-a-profiling-run-into-a-profiling-data-vsp-file"></a>将用于分析运行的符号嵌入到分析数据 (.vsp) 文件

- 在命令提示符窗口中，键入以下命令：

   \<Path><strong>VSPerfReport \<</strong>VSP File> /PackSymbols

   默认采用 .vsp 文件的基名称对 .vsps 文件进行命名 。 可以通过使用“输出”选项指定替代名称。

### <a name="to-create-a-summary-profiling-data-file"></a>创建摘要分析数据文件

- 在命令提示符窗口中，键入以下命令：

   \<Path><strong>VSPerfReport \<</strong>VSP File> /SummaryFile [/Output:\<File Name>] 

   默认采用 .vsp 文件的基名称对 .vsps 文件进行命名 。 可以通过使用“输出”选项指定替代名称。
