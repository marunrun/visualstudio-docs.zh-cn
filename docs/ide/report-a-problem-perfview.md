---
title: 使用 PerfView 收集 ETL 跟踪
ms.date: 09/27/2019
ms.topic: conceptual
helpviewer_keywords:
- perfview
- ETL Trace
author: corob-msft
ms.author: corob
manager: jillfra
dev_langs:
- CSharp
- VB
- CPP
ms.workload:
- multiple
ms.description: Use perfview.exe to collect ETL traces for troubleshooting issues with Visual Studio
ms.openlocfilehash: 24d72e9630506ecc3d25fcc75e51eeb84f619e53
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "77271168"
---
# <a name="collect-an-etl-trace-with-perfview"></a>使用 PerfView 收集 ETL 跟踪

PerfView 是一个基于 [Windows 事件跟踪](/windows/desktop/ETW/event-tracing-portal)创建 ETL（事件跟踪日志）文件的工具，可用于排查 Visual Studio 存在的某些问题类型。 有时，当你报告问题时，产品团队可能会要求你运行 PerfView 以收集其他信息。

## <a name="install-perfview"></a>安装 PerfView

从 [GitHub](https://github.com/Microsoft/perfview/blob/master/documentation/Downloading.md) 下载 PerfView。

## <a name="run-perfview"></a>运行 PerfView

1. 以管理员的身份在 Windows 资源管理器中右键单击“PerfView.exe”  ，然后选择“以管理员身份运行” 
1. 在“收集”菜单上，选择“收集” 
1. 勾选“压缩”  、“合并”  和“线程时间”  。
1. 将“循环 MB”  增加到 1000。
1. 如果要多次收集，请更改“当前目录”  以将 ETL 跟踪保存到指定文件夹和数据文件中。
1. 要开始记录数据，请选择“开始收集”  按钮。
1. 要停止记录数据，请选择“停止收集”  按钮。 PrefView.etl.zip 文件将被保存在指定的目录。

PerfView 只能存储适合其缓冲区的最新数据。 因此，尝试在 Visual Studio 开始冻结或减速后尽快停止收集。 遇到问题后不要收集超过 30 秒。

有关更多信息，请参阅 [Channel9 上的 PerfView 教程](https://channel9.msdn.com/Series/PerfView-Tutorial/PerfView-Tutorial-1-Collecting-data-with-the-Run-command)。
