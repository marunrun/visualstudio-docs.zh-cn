---
title: 使用图形诊断调试计算着色器
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 69287456-644b-4aff-bd03-b1bbb2abb82a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 19ae8472aaafbad1a04485ff2e3a2637f345bc00
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/28/2019
ms.locfileid: "66262865"
---
# <a name="walkthrough-using-graphics-diagnostics-to-debug-a-compute-shader"></a>演练：使用图形诊断来调试计算着色器
本演练演示如何使用 Visual Studio 图形诊断工具来调查生成错误结果的计算着色器。

 此演练阐释了以下任务：

- 使用“图形事件列表”  定位问题的潜在根源。

- 使用“图形事件调用堆栈”确定由 DirectCompute `Dispatch` 事件执行的是哪一个计算着色器  。

- 使用“图形管道阶段”窗口和 HLSL 调试器检查是问题根源的计算着色器  。

## <a name="scenario"></a>方案
 在此方案中，你编写了流体动力学模拟，它利用 DirectCompute 来执行模拟更新的计算量最大的部分。 应用运行时，数据集和用户界面的呈现看起来正常，但模拟未按预期运作。 通过使用“图形诊断”，可以捕获图形日志的问题，以便调试该应用。 应用中的问题如下所示：

 ![模拟的流体的行为不正确。](media/gfx_diag_demo_compute_shader_fluid_problem.png "gfx_diag_demo_compute_shader_fluid_problem")

 有关如何捕获图形日志中的图形问题的信息，请参阅 [Capturing Graphics Information](capturing-graphics-information.md)。

## <a name="investigation"></a>调查
 可以使用“图形诊断”工具加载图形日志文件，以便检查捕获的帧。

#### <a name="to-examine-a-frame-in-a-graphics-log"></a>检查图形日志中的帧

1. 在 Visual Studio 中，加载包含展现出错误模拟结果的帧的图形日志。 Visual Studio 中将出现新的“图形诊断”选项卡。 此选项卡的顶部是所选帧的呈现目标输出。 底部是“帧列表”，显示每个捕获的帧的缩略图  。

2. 在“帧列表”中，选择演示错误模拟行为的帧  。 即使此错误似乎是在模拟代码（而非呈现代码）中，你仍必须选择一个帧，因为 DirectCompute 事件和 Direct3D 事件都是在逐帧的基础上捕获的。 在此方案中，图形日志选项卡如下所示：

    ![图形日志文档在 Visual Studio 中。](media/gfx_diag_demo_compute_shader_fluid_step_1.png "gfx_diag_demo_compute_shader_fluid_step_1")

   选择演示问题的帧后，可以使用“图形事件列表”  进行诊断。 “图形事件列表”包含活动帧期间每个 DirectCompute 调用和 Direct3D API 调用的事件，例如，在 GPU 上运行计算或呈现数据集或 UI 的 API 调用  。 在这种情况下，我们关注的是表示在 GPU 上运行的部分模拟的 `Dispatch` 事件。

#### <a name="to-find-the-dispatch-event-for-the-simulation-update"></a>查找模拟更新的 Dispatch 事件

1. 在“图形诊断”工具栏上，选择“事件列表”，打开“图形事件列表”窗口    。

2. 检查呈现数据集的 draw 事件的“图形事件列表”  。 若要简化此过程，请输入`Draw`中**搜索**右上角的框**图形事件列表**窗口。 这将筛选列表，使其仅包含在其标题中具有的“Draw”的事件。 在此方案中，你将发现发生了以下 draw 事件：

    ![事件列表&#40;EL&#41;显示 draw 事件。](media/gfx_diag_demo_compute_shader_fluid_step_2.png "gfx_diag_demo_compute_shader_fluid_step_2")

3. 查看图形日志文档选项卡中的呈现目标时，请浏览每个 draw 事件。

4. 在呈现目标首次显示呈现的数据集时停止。 在此方案中，在第一个 draw 事件中呈现数据集。 显示模拟中的错误：

    ![此 draw 事件呈现模拟数据集。](media/gfx_diag_demo_compute_shader_fluid_step_3.png "gfx_diag_demo_compute_shader_fluid_step_3")

5. 现在检查更新模拟的 `Dispatch` 事件的“图形事件列表”  。 由于模拟可能在呈现之前就进行了更新，因而可以先关注在呈现结果的 draw 事件之前发生的 `Dispatch` 事件。 若要简化此过程，修改**搜索**框以读取`Draw;Dispatch;CSSetShader(`。 这将筛选列表，使其还包含除 draw 事件以外的 `Dispatch` 和 `CSSetShader` 事件。 在此方案中，你将发现发生在 draw 事件之前的多个 `Dispatch` 事件：

    ![EL 显示 draw、 Dispatch 和 CSSetShader 事件](media/gfx_diag_demo_compute_shader_fluid_step_4.png "gfx_diag_demo_compute_shader_fluid_step_4")

   了解许多 `Dispatch` 事件中的哪几个事件可能对应于该问题后，就可以更详细地对其进行检查。

#### <a name="to-determine-which-compute-shader-a-dispatch-call-executes"></a>确定调度调用执行哪一个计算着色器

1. 在“图形诊断”工具栏上，选择“事件调用堆栈”，以打开“图形事件调用堆栈”窗口    。

2. 从呈现模拟结果的 draw 事件开始，在每个之前的 `CSSetShader` 事件中逐个向后移动。 然后，在“图形事件调用堆栈”窗口中，选择最顶部的函数以定位到调用站点  。 在调用站点，您可以使用的第一个参数[CSSetShader](/windows/desktop/api/d3d11/nf-d3d11-id3d11devicecontext-cssetshader)函数调用，以确定哪个计算着色器执行下一步`Dispatch`事件。

   在此方案中，每个帧中有三对 `CSSetShader` 和 `Dispatch` 事件。 逆向执行，第三对事件表示集成步骤（计算流体粒子的实际移动的步骤），第二对表示力计算步骤（计算影响每个粒子的力的步骤），第一对表示密度计算步骤。

#### <a name="to-debug-the-compute-shader"></a>调试计算着色器

1. 在“图形诊断”工具栏上，选择“管道阶段”，从而打开“图形管道阶段”窗口    。

2. 选择第三个 `Dispatch` 事件（后面紧跟 draw 事件），然后在“图形管道阶段”窗口中的“计算着色器”阶段下选择“开始调试”    。

    ![选择第三个 Dispatch 事件中 EL.](media/gfx_diag_demo_compute_shader_fluid_step_6.png "gfx_diag_demo_compute_shader_fluid_step_6")

    在执行集成步骤的着色器处启动 HLSL 调试器。

3. 检查集成步骤的计算着色器源代码以搜索错误源。 使用“图形诊断”调试 HLSL 计算着色器代码时，可以单步执行代码并使用其他熟悉的调试工具（如监视窗口）。 在此方案中，你确定了在执行集成步骤的计算着色器中似乎没有错误。

    ![调试 IntegrateCS 计算着色器。](media/gfx_diag_demo_compute_shader_fluid_step_7.png "gfx_diag_demo_compute_shader_fluid_step_7")

4. 若要停止调试计算着色器，在**调试**工具栏上，选择**停止调试**(键盘：Shift + F5)。

5. 接下来，请选择第二个 `Dispatch` 事件并开始调试计算着色器，正如在前面的步骤中所进行的操作那样。

    ![选择第二个 Dispatch 事件中 EL.](media/gfx_diag_demo_compute_shader_fluid_step_8.png "gfx_diag_demo_compute_shader_fluid_step_8")

    在计算作用于每个流体粒子的力的着色器处启动 HLSL 调试器。

6. 检查力计算步骤的计算着色器源代码。 在此方案中，你可以确定此处为错误源。

    ![调试 ForceCS&#95;简单的计算着色器。](media/gfx_diag_demo_compute_shader_fluid_step_9.png "gfx_diag_demo_compute_shader_fluid_step_9")

   确定错误的位置之后，可以停止调试并修改计算着色器源代码，以正确地计算相互作用的粒子之间的距离。 在此方案中，只需将行 `float2 diff = N_position + P_position;` 更改为 `float2 diff = N_position - P_position;`：

   ![更正后的计算&#45;着色器代码。](media/gfx_diag_demo_compute_shader_fluid_step_10.png "gfx_diag_demo_compute_shader_fluid_step_10")

   在此方案中，因为计算着色器是在运行时进行编译的，所以在更改后只需重新启动该应用便可观察更改对模拟的影响。 无需重新生成应用。 运行应用时，可发现此时模拟运行正常。

   ![模拟的流体的行为正确。](media/gfx_diag_demo_compute_shader_fluid_resolution.png "gfx_diag_demo_compute_shader_fluid_resolution")