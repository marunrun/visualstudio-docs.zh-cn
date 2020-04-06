---
title: 视觉工作室动画 |微软文档
ms.date: 04/26/2017
ms.topic: conceptual
ms.assetid: 446773a9-e6f7-4c0c-8dbc-9e303bf32eb1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dc11eb7bab69728be5ceaa55143f56e93cd1fca4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80698610"
---
# <a name="animations-for-visual-studio"></a>Visual Studio 的动画
## <a name="animation-fundamentals"></a>动画基础知识

### <a name="animation-best-practices-in-visual-studio"></a>可视化工作室中的动画最佳实践
遵循这些规则，确保整个 Visual Studio IDE 的动画样式一致且用户友好。

- **有选择性。** 将动画限制为用于特定目的的动画。

- **时间和速度对于**确保过渡感觉快速自然非常重要：

  - 在半秒（500 毫秒）内完成动画过渡。

  - 经常发生的动画需要足够快，这样它们就不会中断用户的工作流。 在循环中观看动画并调整计时，直到感觉正确为止。

  - 动画不应该那么快或不和谐，以至于很难理解，但不要那么慢，以至于它让人不耐烦地完成过渡。

  - 使用可变计时来强调重要性。 例如，在类图上导航一系列项目时，快速浏览项之间的转换，然后减慢速度以专注于重要项。

- 使用从一种状态到另一种状态**的渐进非线性缓动**，给人一种平静和自然运动的感觉。

- 如果可能，**请使用悬停上的精细动画**来指示鼠标下方的交互式元素。

- 如果严重依赖要素中的动画，则**提供一种在**"**工具>选项**"对话框中将其在本地（针对所有要素）关闭的方法。

- **一次只能出现一个动画**，只传达一条信息。 多个对象移动或尝试传达多个内容可能会令人困惑。

- **微妙是很重要的。** 在大多数情况下，动画不需要要求用户注意来达到其目的。 时间、顺序和行为的细微变化可能会显著影响感知，并可以区分有效和无效的动画。

- 当使用动画来吸引对某物的注意时 **，请确保它值得打断用户的**思路。

- 通过动画**显示进度或状态时**：

  - 当基础进程未前进时，停止显示进度移动。

  - 区分不确定的流程和确定的进程。

  - 确保动画具有可识别的完成和失败状态。

  - 通过提供实际使用的其他信息，尽量减少显示状态的效果动画的使用，并确保它们具有实际价值。 示例包括瞬态状态更改和紧急情况

#### <a name="animation-donts"></a>动画不：

- 不要使用小运动（在小尺寸内移动）。 首选淡入淡出和更改而不是移动的对象。

- 不要使用发生在大面积的屏幕空间的动画。 无论大小，这种动画样式都会分散用户的注意力。

- 不要使用与用户当前关注的对象或与对象交互无关的动画。

- 不要使用需要用户交互来重置状态的动画，例如强制用户响应闪烁的通知，以便停止闪烁。 以任何方式与他们互动应该足以解雇他们。

有关这些最佳实践的应用程序的详细信息，请参阅[动画模式](../../extensibility/ux-guidelines/animations-for-visual-studio.md#BKMK_AnimationPatterns)。

### <a name="animation-metrics"></a>动画指标

- 系统应在 10 毫秒内对用户手势做出明显响应。

- 动画转换完成的时间不应超过 500 毫秒。

- 补偿需要较长时间的过渡的一种方法是将其分为两部分。 例如，动画的第一部分可以是空内容容器（最多 500 毫秒），然后是内容淡入容器（最多 500 毫秒）。

- 对于可以计算的加载时间，首选决定因素进度指示器（完成进度指标的百分比）。

- 对于无法计算的加载时间，适合使用光标或嵌入式旋转动画（加载或工作指示器）等繁忙指示器。

### <a name="animation-as-communicator"></a>动画作为传播者
在可视化工作室 UI 中，动画仅作为通信工具运行。  它用于传达各种信息，如 UI 中的结构更改（例如，当菜单打开或关闭时）。 动画可以帮助可视化复杂系统的时间相关行为，如安装进度可视化。 动画还可用于通过警报和通知吸引注意力。

 UI 动画通常以四种方式运行：可视化、吸引注意力、模拟和响应时间/进度指示器。

#### <a name="visualize"></a>可视化
动画可以强调对象的三维性质，使用户更容易可视化其空间结构。 为此，动画可能需要将对象旋转成一个完整的圆，缓慢地来回旋转，或者使对象更近，并稍微增加其大小以强调翻转或焦点。

尽管可以使用用户控件移动三维对象，但设计人员应提前（以编程或手动方式）确定如何最好地为运动设置动画，以便对对象进行最佳理解。 然后，用户可以通过将光标放在对象上来激活此编程动画，而用户控制的移动要求用户了解如何操作对象。 将移动限制为一次的单个轴或方向;缩放、旋转或平移，但同时执行多个操作。

可视化类别包括数据、关系、状态、结构、顺序和时间的各个方面。

##### <a name="data"></a>数据
说明复杂和可变的信息：

- 浏览图表和图形等信息可视化效果

- 单步执行序列、导游和分页

- 调用详细信息、指向和突出显示特定信息

- 叠加焦点元素顶部的细节和其他信息

- 从一个结构或组织表示形式转变为另一个结构或组织代表

- 使用时间滑块、慢跑和穿梭轮以及运输控制（播放、停止和暂停）表示随时间的变化

##### <a name="relationships"></a>关系

- 说明项目如何彼此关联，或哪些项目与给定项目相关

- 显示层次结构和父子或兄弟姐妹关系

- 一个元素生成另一个元素

- 一个元素最小化到另一个元素

- 一个元素被拴在另一个元素上

##### <a name="state"></a>状态

- 内容更新

- 用户焦点和选择

- 进度

- 错误

##### <a name="structure"></a>结构

- 在一个节点上透视结构

- 调整方向

- 最小化和最大化，或展开和折叠

##### <a name="sequence"></a>序列

- 幻灯片放映序列

- 翻阅图片

##### <a name="time"></a>时间

- 显示随时间推移、时间推移和截屏的更改

- 移动到垃圾、撤消和重做

- 恢复历史状态

#### <a name="attract-attention"></a>吸引注意力
如果目标是将用户的注意力吸引到多个元素中的单个元素，或提醒用户更新信息，则动画可能是合适的。 例如，应用程序起始页可能使用"入门"按钮，该按钮在页面加载后滑入到位。

通常，屏幕上的最后一个移动元素会吸引用户的注意。  在一系列动画元素中，用户的注意力将跟随最后一个移动对象。

##### <a name="alert"></a>警报

- 提醒用户，引起注意，显示进度

- 显示某些操作执行正确或不正确，或显示进度或进度更改

- 在任务期间提示用户，例如联机查找更多信息或了解有关当前任务的信息

##### <a name="notifications"></a>通知

- 提醒用户有关错误条件

- 中断用户以查看他们是否想关注其他内容

- 轻轻地通知用户进程已完成或更改，例如下载完成时。

#### <a name="simulate"></a>Simulate
此类别涵盖物理性和维度性。

- 说明对象来自何处或它们去向何处

- 展开和折叠或打开和关闭

- 平移、滚动和页面翻页

- 堆叠和 z 排序

- 旋转木马和手风琴

- 翻转和旋转 UI

#### <a name="response-and-progress-indicators"></a>反应和进度指标
进度指标有几个显著的优势：

- 确定进度指标和不确定进度指示器都向用户保证系统尚未崩溃，并且正在处理该问题。

- 确定指标使用户了解操作的进展有多远，以及接近完成的感觉。

## <a name="animation-patterns"></a><a name="BKMK_AnimationPatterns"></a>动画模式

### <a name="overview"></a>概述
Visual Studio 中的动画旨在在不妨碍用户工作效率的情况下提供特定功能。 通常，可视化工作室中的动画应该是：

- 小而不显眼

- 自然和现实

- 微妙和柔和

- 快速高效

- 放松，不匆忙

此图显示了我们为 Visual Studio 推荐的动画样式。 没有动画或微妙的动画，如淡入淡出/淡出是最常用的。 运动动画（如扩展和收缩、X 和 Y 位置更改以及旋转）的应用有限。

![Visual Studio 的建议动画样式](../../extensibility/ux-guidelines/media/1202-a_vsanimstyles.png "1202-a_VSAnimStyles")<br />Visual Studio 的建议动画样式

#### <a name="appear-and-disappear"></a>出现并消失
使用此模式，元素从可见切换到视图外，无需过渡动画即可返回。

![显示和消失动画](../../extensibility/ux-guidelines/media/1202-b_appearanddisappear.png "1202-b_AppearAndDisappear")<br />显示和消失动画

##### <a name="correct-usage"></a>正确的用法
需要立即显示或消失的新鲜 UI 元素，以便用户不会分心或受阻。 此外，慢动作动画可能被视为性能拖动，这在显示和消失样式中不会发生。

##### <a name="incorrect-usage"></a>使用不正确
UI 突然出现，用户不知道发生了什么，添加动画将有助于上下文理解。

##### <a name="animation-properties"></a>动画属性
时间延迟通常为零秒。

##### <a name="examples"></a>示例
- 自动隐藏工具窗口

- 键盘激活编辑器 UI，如智能感知和参数帮助

- 扩展和折叠代码区域

#### <a name="fade-in-and-fade-out"></a>淡入淡出
使用此模式，UI 元素从不可见（0% 不公开性）转换为可见（100% 不公开性），反之亦然。

![淡入和淡出动画](../../extensibility/ux-guidelines/media/1202-c_fadeinfadeout.png "1202-c_FadeInFadeOut")<br />淡入和淡出动画

##### <a name="correct-usage"></a>正确的用法
这是最常推荐的 UI 动画。 这是一种微妙的效果，在不中断流量的情况下增加兴趣。 在某些情况下，用户甚至可能没有意识到有一个动画，感知一个平滑和流动的 UI 系统。

##### <a name="animation-properties"></a>动画属性

- 开始不一用性：0%用于淡入，100%用于淡出

- 结束不成性：100%用于淡入，0%用于淡出

- 持续时间：独立 200 毫秒，用作组合动画序列的一部分时为 100 毫秒

- 放松风格：因内

##### <a name="examples"></a>示例

- 自动隐藏工具窗口

- 菜单打开和关闭

- 背景和前景选项卡过渡

#### <a name="color-blend-from-a-to-b"></a>颜色混合从 A 到 B
使用此模式，UI 元素从颜色 A 更改为颜色 B。

![颜色混合动画](../../extensibility/ux-guidelines/media/1202-d_colorblend.png "1202-d_ColorBlend")<br />颜色混合动画

##### <a name="correct-usage"></a>正确的用法
当 UI 元素将颜色从一个上下文或状态更改为另一个上下文或状态时，作为动画过渡。

##### <a name="animation-properties"></a>动画属性

- 起始颜色：特定于 UI

- 结束颜色：特定于 UI

- 持续时间：独立 200 毫秒，用作组合动画序列的一部分时为 100 毫秒

- 放松风格：因内

##### <a name="examples"></a>示例

- 文档窗口状态转换（活动、上次活动和非活动）

- 工具窗口状态转换（聚焦和非焦点）

#### <a name="expand-and-contract"></a>扩展和收缩
使用此模式，UI 元素在 X、Y 或两个方向中展开。

![展开和收缩动画](../../extensibility/ux-guidelines/media/1202-e_expandcontract.png "1202-e_ExpandContract")<br />展开和收缩动画

##### <a name="correct-usage"></a>正确的用法
当 UI 元素将大小从一个上下文更改为另一个上下文时，作为动画过渡。

##### <a name="animation-properties"></a>动画属性

- X 比例：% 或特定尺寸（以像素为单位）

- Y 比例：% 或特定尺寸（以像素为单位）

- 锚点位置：一般左上角（从左到右语言）或右上方（对于从右到左的语言）

- 持续时间：独立 200 毫秒，用作组合动画序列的一部分时为 100 毫秒

##### <a name="examples"></a>示例

- 体系结构资源管理器面板展开和折叠

- 可视化工作室 2017 起始页项目展开和折叠

#### <a name="x-y-position-change"></a>X-Y 位置变化
使用此模式，UI 元素将更改其 X 或 Y 位置或两者。

![X-Y 位置更改动画](../../extensibility/ux-guidelines/media/1202-f_xypositionchange.png "1202-f_XYPositionChange")<br />X-Y 位置更改动画

##### <a name="correct-usage"></a>正确的用法
当 UI 元素将位置从一个上下文更改为另一个上下文时，作为动画过渡。

##### <a name="animation-properties"></a>动画属性

- 启动 X 和 Y 位置：特定于 UI

- 结束 X 和 Y 位置：特定于 UI

- 运动路径：无

- 持续时间：独立 200 毫秒，用作组合动画序列的一部分时为 100 毫秒

- 放松风格：因内

##### <a name="example"></a>示例
选项卡重新排序

#### <a name="rotate"></a>旋转
使用此模式，UI 元素将旋转。

![UI 元素旋转动画](../../extensibility/ux-guidelines/media/1202-g_rotate.png "1202-g_Rotate")<br />UI 元素旋转动画

##### <a name="correct-usage"></a>正确的用法
仅适用于不确定的旋转进度指示器。

##### <a name="animation-properties"></a>动画属性

- 旋转程度： 360

- 旋转中心：对象中间

- 持续时间：连续

##### <a name="example"></a>示例
不确定进度指示器（旋转）

### <a name="common-shell-ui-actions-and-recommended-animations"></a>常见的 shell UI 操作和建议的动画

#### <a name="tab-open"></a>选项卡打开
![选项卡打开动画](../../extensibility/ux-guidelines/media/1202-h_tabopen.png "1202-h_TabOpen")<br />选项卡打开动画

- 样式：显示

- 持续时间：零秒

#### <a name="tab-close"></a>选项卡关闭
![选项卡关闭动画](../../extensibility/ux-guidelines/media/1202-i_tabclose.png "1202-i_TabClose")<br />选项卡关闭动画

- 样式：X 位置变化

- 持续时间： 200 毫秒

#### <a name="tab-reorder"></a>选项卡重新排序
![Visual Studio 中的选项卡重新排序动画](../../extensibility/ux-guidelines/media/1202-j_tabreorder.png "1202-j_TabReorder")<br />选项卡重新排序动画

- 样式：X 位置变化

- 持续时间： 200 毫秒

#### <a name="close-floating-document"></a>关闭浮动文档
![关闭浮动文档动画](../../extensibility/ux-guidelines/media/1202-k_closefloatingdocument.png "1202-k_CloseFloatingDocument")<br />关闭浮动文档动画

- 样式：显示

- 持续时间： 200 毫秒

#### <a name="window-state-transition"></a>窗口状态转换
![窗口状态过渡动画](../../extensibility/ux-guidelines/media/1202-l_windowstatetransition.png "1202-l_WindowStateTransition")<br />窗口状态过渡动画

- 样式：要与其他窗口一致，让当前操作系统定义文档关闭动画。

- 持续时间： 200 毫秒

#### <a name="menu-open"></a>菜单打开
![菜单打开动画](../../extensibility/ux-guidelines/media/1202-m_menuopen.png "1202-m_MenuOpen")<br />菜单打开动画

- 样式：淡入

- 持续时间： 200 毫秒

#### <a name="menu-close"></a>菜单关闭
![菜单关闭动画](../../extensibility/ux-guidelines/media/1202-n_menuclose.png "1202-n_MenuClose")<br />菜单关闭动画

- 样式：淡出

- 持续时间： 200 毫秒

#### <a name="auto-hide-tool-window-reveal"></a>自动隐藏工具窗口显示
![自动隐藏工具窗口显示动画](../../extensibility/ux-guidelines/media/1202-o_autohidetoolwindowreveal.png "1202-o_AutoHideToolWindowReveal")<br />自动隐藏工具窗口显示动画

- 样式：显示

- 持续时间：零秒
