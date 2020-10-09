---
title: Visual Studio 中的 DirectX 12 支持 | Microsoft Docs
description: 建议 DirectX 12 用户在 Windows 上使用PIX，获得完整的图形调试体验
ms.date: 09/29/2020
ms.topic: conceptual
author: davidcongruili
ms.author: davidli1
manager: mluparu
ms.workload:
- multiple
ms.openlocfilehash: 9dbc52a0233abe467da4d41af0134663bc7cd9df
ms.sourcegitcommit: a1cb4e2025045c2ad79167645c4c0f33b94b1152
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2020
ms.locfileid: "91671413"
---
# <a name="directx-12-support-in-visual-studio"></a>Visual Studio 中的 DirectX 12 支持

## <a name="directx-12-support"></a>DirectX 12 支持

Visual Studio 图形诊断不支持 DirectX 12 游戏。 对于具有完全 DirectX 12 支持的图形调试，Visual Studio 建议使用“Windows 上的 PIX”。 

Windows 上的 PIX 是一个具有远程功能的性能优化和调试工具。 Windows 上的 PIX 提供可满足图形调试需求的七个主要功能。 通过 GPU 捕获调试和分析 Direct3D 12 图形渲染的性能。 通过计时捕获了解游戏执行的所有 CPU 和 GPU 工作的性能和线程处理。 通过文件 IO 捕获识别游戏的磁盘 IO 模式和包布局中的低效之处。

使用 [Windows上的 PIX](https://aka.ms/PIXonWindows) 推进你的图形调试之旅。

[下载 Windows上的 PIX](https://aka.ms/downloadPIX) 或[查看文档](https://devblogs.microsoft.com/pix/documentation/) 。

## <a name="pix-on-windows"></a>Windows 上的 PIX

Windows 上的 PIX 有七种主要的操作模式：
1. GPU 捕获，用于调试和分析 Direct3D 12 图形渲染的性能。
2. 计时捕获，用于了解游戏执行的所有 CPU 和 GPU 工作的性能和线程处理，以及用于跟踪 GPU 内存使用情况。
3. 函数摘要捕获可累积关于每个函数运行多长时间以及调用频率的信息。
4. 调用图捕获可跟踪单个函数的执行。
5. 内存分配捕获可让你深入了解游戏执行的内存分配。
6. 文件 IO 捕获有助于识别游戏的磁盘 IO 模式和包布局中的低效之处。
7. 系统监视器可在游戏运行时显示实时计数器数据。

有关 Windows 上的 PIX 的详细视频介绍，请参阅[此处](https://www.youtube.com/playlist?list=PLeHvwXyqearWuPPxh6T03iwX-McPG5LkB)
