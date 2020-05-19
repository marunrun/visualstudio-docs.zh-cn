---
title: 图形诊断示例 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 45dd86b2-801e-4b07-a8c4-7bd25641d7f8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4df2fafb523d04a8ec222b10e1ac9ed3aa95454d
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2019
ms.locfileid: "73187928"
---
# <a name="graphics-diagnostics-examples"></a>图形诊断示例
以下示例显示如何使用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 图形诊断调试基于 DirectX 的应用中的呈现问题。

## <a name="capturing-graphics-information"></a>捕获图形信息
 在可以使用图形诊断来诊断应用中的呈现问题之前，必须在应用运行时从应用中捕获图形信息。 可以从正在本地运行的应用或从正在远程计算机或其他设备上运行的应用中捕获图形信息。 以下演练演示如何通过手动方式或编程方式从应用中捕获图形信息：

- [演练：捕获图形信息](walkthrough-capturing-graphics-information.md)

- [演练：以编程方式捕获图形信息](walkthrough-capturing-graphics-information-programmatically.md)

## <a name="use-graphics-diagnostics-with-an-arm-based-device"></a>将图形诊断用于基于 ARM 的设备
 通过使用远程调试，你可以使用图形诊断调试基于 ARM 的设备上的 Direct3D 应用。 有关详细信息，请参阅[操作说明：将图形诊断用于 ARM 设备](graphics-diagnostics-examples.md)。

## <a name="playing-back-graphics-information"></a>播放图形信息
 从运行的应用中捕获图形信息之后，你可以播放捕获的事件以诊断呈现问题。 若要进行播放，你可以使用你的开发计算机，或使用连接到的远程计算机或设备。 有关详细信息，请参阅[如何：更改图形诊断播放计算机](how-to-change-the-graphics-diagnostics-playback-machine.md)。

## <a name="debugging-missing-objects"></a>调试缺少的对象
 缺少一个对象（或多个对象）是图形开发人员遇到的最常见的呈现问题之一。 这种问题很难诊断，因为几种不同种类的错误可能会导致对象明显地消失。 缺少对象的典型原因包括设备状态配置不正确、转换对象的几何图形出现问题，或图形管道配置不正确。

 以下方案演示如何使用图形诊断确定缺少对象的原因，并查找有关代码。

- [演练：因设备状态而缺少对象](walkthrough-missing-objects-due-to-device-state.md)

- [演练：因顶点着色而缺少对象](walkthrough-missing-objects-due-to-vertex-shading.md)

- [演练：因管道误配置而缺少对象](walkthrough-missing-objects-due-to-misconfigured-pipeline.md)

## <a name="debugging-rendering-errors"></a>调试呈现错误
 一个对象（或多个对象）具有的外观不正确是图形开发人员遇到的另一个常见问题。 这种问题很难诊断，因为不正确的外观及其成因可能非常明显（绑定了错误纹理），也可能难以捉摸（着色器代码中的 Bug 或着色器之间的意外交互）。 某些问题可能是由一组错误导致的。

 以下方案演示如何使用图形诊断跟踪由较小的着色器 Bug 引起的不太难捉摸的呈现问题：

- [演练：调试因着色引起的呈现错误](walkthrough-debugging-rendering-errors-due-to-shading.md)

## <a name="debugging-compute-shaders"></a>调试计算着色器
 可以使用图形诊断调试产生不正确结果的 DirectCompute 计算着色器内核。 借助 DirectCompute，你可以使用 GPU 的计算能力，以并行执行大量数据元素上的计算。 对于某些种类的问题，可以多次执行使用 GPU，速度甚至比良好优化过的 CPU 代码还快。 但是，传统的调试器无法检测在 GPU 上运行的代码。 调试此种代码需要专用工具，这些工具通常特定于供应商，而且可能不会与 Visual Studio 很好地集成。 为了使计算着色器调试在 GPU 范围内更为一致，图形诊断将捕获 DirectCompute 调度事件（包括 Direct3D 呈现事件），以便你可以使用熟悉的工具调试计算着色器代码中的问题。

 有关演示如何调试由计算着色器中的 Bug 导致的模拟问题的方案，请参阅[演练：使用图形诊断来调试计算着色器](walkthrough-using-graphics-diagnostics-to-debug-a-compute-shader.md)。