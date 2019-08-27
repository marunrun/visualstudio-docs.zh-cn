---
title: 演练：调试因着色引起的呈现错误 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 01875b05-cc7b-4add-afba-f2b776f86974
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 44e542bcbb801ee4035ba501b50bad81b53e8bdf
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62849294"
---
# <a name="walkthrough-debugging-rendering-errors-due-to-shading"></a>演练：调试因着色引起的呈现错误
本演练演示如何使用[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]图形诊断工具调查由于着色器 bug 而错误着色的对象。

 本演练演示了如何：

- 检查图形日志文档来标识显示问题的像素。

- 使用“图形像素历史记录”  窗口进一步检查像素状态。

- 使用“HLSL 调试器”  检查像素和顶点着色器。

## <a name="scenario"></a>方案
 当顶点着色器向像素着色器传递不正确或不完整的信息时，通常会在对象上错误着色。

 在此方案中，你最近添加到您的应用程序对象。 您还添加了新顶点和像素着色器以转换该对象并为其提供唯一外观。 在测试过程中运行该应用时，该对象将呈现为纯黑色。 通过使用“图形诊断”，捕获图形日志的问题，以便调试该应用。 问题看起来像此应用程序中的映像：

 ![使用颜色不正确呈现的对象。](media/gfx_diag_demo_render_error_shader_problem.png "gfx_diag_demo_render_error_shader_problem")

## <a name="investigation"></a>调查
 通过使用图形诊断工具，您可以加载图形日志文档以检测测试期间已捕获的帧。

#### <a name="to-examine-a-frame-in-a-graphics-log"></a>检查图形日志中的帧

1. 在[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]，加载包含显示缺少模型的帧的图形日志。 中将显示新的图形日志文档窗口[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。 此窗口的顶部是所选帧的呈现目标输出。 底部是“帧列表” ，以缩略图的形式显示每个捕获的帧。

2. 在中**帧列表**，选择在其中的对象不具有正确的外观的帧。 更新呈现目标以反映所选的帧。 在此方案中，图形日志文档窗口如下所示此映像：

    ![图形日志文档在 Visual Studio 中。](media/gfx_diag_demo_render_error_shader_step_1.png "gfx_diag_demo_render_error_shader_step_1")

   选择演示问题的帧后，可以使用“图形像素历史记录”  窗口进行诊断。 “图形像素历史记录”  窗口将按时间顺序显示可能已对特定像素、其着色器及其呈现器目标产生影响的基元。

#### <a name="to-examine-a-pixel"></a>检查像素

1. 打开“图形像素历史记录”  窗口。 在“图形诊断”  工具栏上，选择“像素历史记录” 。

2. 选择要检查的像素。 在图形日志文档窗口上，选择未正确着色的对象上的某个像素：

    ![选择一个像素会显示有关其历史记录的信息。](media/gfx_diag_demo_render_error_shader_step_2.png "gfx_diag_demo_render_error_shader_step_2")

    将更新“图形像素历史记录”  窗口以反映所选像素。 在此方案中，“图形像素历史记录”  窗口如下所示：

    ![像素历史记录显示一个 DrawIndexed 事件。](media/gfx_diag_demo_render_error_shader_step_3.png "gfx_diag_demo_render_error_shader_step_3")

    请注意，像素着色器的结果是完全不透明的黑色 （0，0，0，1），而**输出合并器**结合使用此像素着色器**上一步**这样的像素颜色的**结果**也是完全不透明的黑色。

   检查错误着色的像素并发现像素着色器输出不是预期的颜色后，可以使用 HLSL 调试器检查像素着色器，找出对象的颜色发生的问题。 你可以使用 HLSL 调试器检查 HLSL 变量在执行期间的状态，分步执行 HLSL 代码，并设置断点以帮助诊断问题。

#### <a name="to-examine-the-pixel-shader"></a>检查像素着色器

1. 开始调试像素着色器。 在“图形像素历史记录”  窗口中，在该对象的基元之下“像素着色器” 旁，选择“启动调试”  按钮。

2. 在此方案中，由于像素着色器仅传递来自顶点着色器的颜色，因此很容易注意到像素着色器并非问题根源。

3. 将指针停留在 `input.color`之上。 请注意，其值是完全不透明黑 (0, 0, 0, 1)。

    !["输入"的"color"成员为黑色。](media/gfx_diag_demo_render_error_shader_step_5.png "gfx_diag_demo_render_error_shader_step_5")

    在此方案中，检查指示不正确的颜色可能是顶点着色器未对要操作的像素着色器提供正确的颜色信息所导致的结果。

   在您确定顶点着色器可能未向像素着色器提供正确信息后，下一步是检查顶点着色器。

#### <a name="to-examine-the-vertex-shader"></a>检查顶点着色器

1. 开始调试顶点着色器。 在“图形像素历史记录”  窗口中，在该对象的基元之下“顶点着色器” 旁，选择“启动调试”  按钮。

2. 找到顶点着色器的输出结构，它是像素着色器的输入。 在这种情况下，此结构名为 `output`。 检查顶点着色器代码，您会发现 `color` 结构的 `output` 成员已显式设置为完全不透明黑，可能是某人进行调试所产生的结果。

3. 确认绝不会从输入结构中复制颜色成员。 由于 `output.color` 的值仅在返回 `output` 结构之前设置为完全不透明黑，因此最好确保在上一行上没有正确初始化 `output` 的值。 在您看到 `output.color` 的值时，逐句通过顶点着色器代码，直至到达将 `output.color`设置为黑色的行。 请注意，在 `output.color` 设置为黑色之前，其值不进行初始化。 这可确认应修改而不是删除将 `output.color` 设置为黑色的代码行。

    !["Output.color"的值为黑色。](media/gfx_diag_demo_render_error_shader_step_7.png "gfx_diag_demo_render_error_shader_step_7")

   在确定导致出现呈现问题的原因是顶点着色器未向像素着色器提供正确的颜色值之后，您可使用此信息来修复问题。 在此方案中，您可通过更改顶点着色器中的以下代码来修复问题

```hlsl
output.color = float3(0.0f, 0.0f, 0.0f);
```

 更改为

```hlsl
output.color = input.color;
```

 此代码仅传递来自该对象未经修改的顶点的颜色 - 更复杂的顶点着色器可以在传递颜色之前对其进行修改。 已更正的顶点着色器代码应如下所示：

 ![已更正的顶点着色器代码。](media/gfx_diag_demo_render_error_shader_step_8.png "gfx_diag_demo_render_error_shader_step_8")

 修复代码后，重新生成并运行应用以查明呈现的问题是否已解决。

 ![使用的颜色正确呈现的对象。](media/gfx_diag_demo_render_error_shader_resolution.png "gfx_diag_demo_render_error_shader_resolution")
