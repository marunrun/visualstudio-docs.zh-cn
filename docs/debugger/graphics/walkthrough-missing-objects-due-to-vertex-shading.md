---
title: 演练：因顶点着色而缺少对象 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: e42b54a0-8092-455c-945b-9ecafb129d93
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cc3bd288044c9fea1da648b64cabc87148b8463a
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388603"
---
# <a name="walkthrough-missing-objects-due-to-vertex-shading"></a>演练：因顶点着色而缺少对象
本演练演示了如何使用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 图形诊断工具调查因顶点着色器阶段出现的错误而缺少的对象。

 此演练阐释了以下任务：

- 使用“图形事件列表”  定位问题的潜在根源。

- 使用“图形管道阶段”  窗口检查 `DrawIndexed` Direct3D API 调用的影响。

- 使用“HLSL 调试器”  检查顶点着色器。

- 使用“图形事件调用堆栈”  帮助查找错误 HLSL 常量的源。

## <a name="scenario"></a>方案
 当顶点着色器以不正确或意外的方式变换对象顶点的形状时，会出现三维应用中缺少对象的一个常见原因 — 例如，对象可能缩放到很小的尺寸或变形而导致出现在照相机后面而不是前面。

 在此方案中，当应用程序运行测试时，背景如预期呈现，但是，其中一个对象不会出现。 通过使用“图形诊断”，捕获图形日志的问题，以便调试该应用。 应用中的问题如下所示：

 ![不会看到对象。](media/gfx_diag_demo_missing_object_shader_problem.png "gfx_diag_demo_missing_object_shader_problem")

## <a name="investigation"></a>调查
 通过使用图形诊断工具，你可以加载图形日志文件以检测测试期间捕获的帧。

#### <a name="to-examine-a-frame-in-a-graphics-log"></a>检查图形日志中的帧

1. 在 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]中，加载包含显示缺少对象的帧的图形日志。 新的图形日志选项卡将出现在 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]中。 此选项卡的顶部是所选帧的呈现目标输出。 底部是“帧列表” ，以缩略图的形式显示每个捕获的帧。

2. 在“帧列表” 中，选择演示未显示该对象的帧。 更新呈现目标以反映所选的帧。 在此方案中，图形日志选项卡如下所示：

    ![Visual Studio 中的图形日志文档](media/gfx_diag_demo_missing_object_shader_step_1.png "gfx_diag_demo_missing_object_shader_step_1")

   选择演示问题的帧后，可以使用“图形事件列表” 开始进行诊断。 “图形事件列表”  包含用以呈现活动帧的各个 Direct3D API 调用，例如设置设备状态、创建和更新缓冲区、绘制在帧中显示的对象的 API 调用。 许多类型的调用（例如绘图、调度、复制或清除调用）都很有趣，因为当应用按照预期运行时通常（但不总是）在呈现目标中会有相应的变动。 绘图调用特别有趣，因为每个绘图调用都表示应用呈现的几何图形（调度调用也可呈现几何图形）。

   由于已知（在本例中）不会将缺失的对象绘制到呈现目标，但会按预期绘制场景的其余部分，因此可以使用“图形事件列表”  和“图形管道阶段”  工具确定与缺失对象的几何图形对应的绘图调用。 “图形管道阶段”  窗口显示已发送到每个绘图调用的几何图形，而不考虑其在呈现目标的效果。 当你进行绘图调用时，将更新管道阶段以显示与该调用相关联的几何图形，并且更新呈现目标输出以显示调用完成后该呈现目标的状态。

#### <a name="to-find-the-draw-call-for-the-missing-geometry"></a>查找缺失的几何图形的绘图调用

1. 打开“图形事件列表”  窗口。 在“图形诊断”  工具栏上，选择“事件列表” 。

2. 打开“图形管道阶段”  窗口。 在“图形诊断”  工具栏上，选择“管道阶段” 。

3. 当通过“图形事件列表”  窗口中的每个绘图调用时，监视“图形管道阶段”  窗口以获知缺失对象。 若要简化此过程，请在“图形事件列表”  窗口右上角的“搜索”  框中输入“Draw”。 这将筛选列表，使其仅包含在其标题中具有的“Draw”的事件。

    在“图形管道阶段”  窗口中，“输入装配器”  阶段将显示转换前的对象的几何图形，而“顶点着色器”  阶段显示转换后的相同对象。 在此方案中，当“输入装配器”  阶段中显示缺失的对象而“顶点着色器”  阶段中不显示任何项目时，即可知已找到该对象。

   > [!NOTE]
   > 如果其他几何阶段（例如外壳着色器、域着色器或几何着色器阶段）处理该对象，则这些阶段可能是问题的原因。 通常情况下，该问题与结果未显示或以意外方式显示的最早阶段相关联。

4. 当到达对应于缺失对象的绘图调用时即停止。 在此方案中，“图形管道阶段”  窗口指示几何图形发布到 GPU（由存在“输入装配器”缩略图指示），但由于在顶点着色器阶段出现问题而未显示于呈现目标中（由“顶点着色器”缩略图指示）。

    ![继续 DrawIndexed 事件并在管道上的其效果](media/gfx_diag_demo_missing_object_shader_step_2.png "gfx_diag_demo_missing_object_shader_step_2")

   在确认该应用被分配为缺失对象的几何图形的绘制调用并在顶点着色器阶段期间出现问题之后，可以使用 HLSL 调试器检查顶点着色器，查明对象的几何图形发生了什么情况。 你可以使用 HLSL 调试器检查 HLSL 变量在执行期间的状态，分步执行 HLSL 代码，并设置断点以帮助诊断问题。

#### <a name="to-examine-the-vertex-shader"></a>检查顶点着色器

1. 开始调试顶点着色器阶段。 在“图形管道阶段”  窗口中的“顶点着色器”  阶段之下，选择“开始调试”  按钮。

2. 由于“输入装配器”  阶段似乎将向顶点着色器提供良好的数据而“顶点着色器”  阶段似乎不会生成任何输出，因此需要检查顶点着色器的输出结构，即 `output`。 由于采用的是分步执行 HLSL 代码，因此，可以在修改 `output` 时仔细查看。

3. 第一次修改 `output` 时，写入成员 `worldPos` 。

    !["Output.worldPos"的值显示合理](media/gfx_diag_demo_missing_object_shader_step_4.png "gfx_diag_demo_missing_object_shader_step_4")

    由于其值看起来是合理的，因此将继续分步执行代码，直至修改 `output`的下一行。

4. 下一次修改 `output` 时，写入成员 `pos` 。

    !["Output.pos"的值清](media/gfx_diag_demo_missing_object_shader_step_5.png "gfx_diag_demo_missing_object_shader_step_5")

    这一次， `pos` 成员的值全部为零，这看上去很可疑。 接下来，你需要确定 `output.pos` 的值为什么全为零。

5. 你注意到， `output.pos` 从名为 `temp`的变量获取其值。 在上一行中，可以看到 `temp` 的值是其上一个值乘以名为 `projection`的常量所得的结果。 怀疑 `temp`的可疑值是否是此乘积的结果。 将指针停留在 `projection`之上时，即可注意到其值也全为零。

    ![投影矩阵包含错误的转换](media/gfx_diag_demo_missing_object_shader_step_6.png "gfx_diag_demo_missing_object_shader_step_6")

    在此方案中，检查显示 `temp`的可疑值很可能是乘以 `projection`而导致的；而由于 `projection` 是用于包含投影矩阵的常量，因此它包含的所有值不应全部为零。

   确定 HLSL 常量 `projection`（由你的应用传递给着色器）是可能的问题源头后，下一步是找到应用的源代码中填充了常量缓冲区的位置。 可以使用“图形事件调用堆栈”  查找此位置。

#### <a name="to-find-where-the-constant-is-set-in-your-apps-source-code"></a>在应用的源代码中查找设置该常量的位置

1. 打开“图形事件调用堆栈”  窗口。 在“图形诊断”  工具栏上，选择“图形事件调用堆栈” 。

2. 在调用堆栈中向上导航到应用的源代码。 在“图形事件调用堆栈”  窗口中，选择最顶层调用以查看是否在该处填充了常量缓冲区。 如果不是，则在调用堆栈中继续向上查找，直至找到填充位置。 在此方案中，你将发现常量缓冲区是在堆栈的更上级处名为 `UpdateSubresource` 的函数中，通过使用 `MarbleMaze::Render`Direct3D API 填充的，并且其值来自名为 `m_marbleConstantBufferData`的常量缓冲区对象：

    ![设置对象的常量缓冲区的代码](media/gfx_diag_demo_missing_object_shader_step_7.png "gfx_diag_demo_missing_object_shader_step_7")

   > [!TIP]
   > 如果同时调试你的应用，则可以在此位置设置一个断点，在呈现下一帧时将命中该断点。 你随后还可以检查 `m_marbleConstantBufferData` 的成员，以确认填充常量缓冲区后是否已将 `projection` 成员的值设置为全零。

   找到填充常量缓冲区的位置，并发现其值来自变量 `m_marbleConstantBufferData` 之后，下一步是找出将 `m_marbleConstantBufferData.projection` 成员设置为全零的位置。 可以使用“查找所有引用”  快速扫描更改 `m_marbleConstantBufferData.projection`的值的代码。

#### <a name="to-find-where-the-projection-member-is-set-in-your-apps-source-code"></a>在应用的源代码中查找设置投影成员的位置

1. 查找对 `m_marbleConstantBufferData.projection`的引用。 打开变量 `m_marbleConstantBufferData`的快捷菜单，然后选择“查找所有引用” 。

2. 若要导航到应用的源代码中修改 `projection` 成员的行位置，请在“查找符号结果”  窗口中选择该行。 由于修改投影成员的第一个结果可能不是问题的原因，因此你可能必须检查应用源代码中的多个区域。

   找到设置 `m_marbleConstantBufferData.projection` 的位置后，你可以检查周围的源代码以确定错误值的起源。 在此方案中，你将发现 `m_marbleConstantBufferData.projection` 的值在初始化为由下一行中的代码 `projection` 给定的值之前，已被设置为名为 `m_camera->GetProjection(&projection);` 的本地变量。

   ![在初始化之前设置大理石投影](media/gfx_diag_demo_missing_object_shader_step_9.png "gfx_diag_demo_missing_object_shader_step_9")

   若要解决此问题，可将设置 `m_marbleConstantBufferData.projection` 的值的代码行移动到对局部变量 `projection`的值进行初始化的行之后。

   ![已更正的 C&#43; &#43;源代码](media/gfx_diag_demo_missing_object_shader_step_10.png "gfx_diag_demo_missing_object_shader_step_10")

   修复代码后，你可以重新生成并运行应用以查明呈现的问题是否已解决：

   ![现在该对象显示。](media/gfx_diag_demo_missing_object_shader_resolution.png "gfx_diag_demo_missing_object_shader_resolution")