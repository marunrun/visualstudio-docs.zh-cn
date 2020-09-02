---
title: Visual Studio 的动画 |Microsoft Docs
ms.date: 04/26/2017
ms.topic: conceptual
ms.assetid: 446773a9-e6f7-4c0c-8dbc-9e303bf32eb1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dc11eb7bab69728be5ceaa55143f56e93cd1fca4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80698610"
---
# <a name="animations-for-visual-studio"></a>Visual Studio 的动画
## <a name="animation-fundamentals"></a>动画基础知识

### <a name="animation-best-practices-in-visual-studio"></a>Visual Studio 中的动画最佳做法
遵循这些规则可确保跨 Visual Studio IDE 的一致和用户友好的动画样式。

- **请选择。** 将动画限制为特定用途的动画。

- **计时和速度非常重要** ，可确保转换的外观迅速和自然：

  - 在半秒 (500 毫秒内完成动画转换) 。

  - 经常需要快速执行的动画将不会中断用户的工作流。 观看循环中的动画并调整计时，直到感觉正确为止。

  - 动画不应太快或 jarring，难以理解，但不太慢，因为它会使一个缺乏耐心完成转换。

  - 使用可变计时来强调重要性。 例如，当在类图上通过一系列项进行导航时，将加快项之间的转换速度，并使其更慢，以重点关注重要项。

- 从一种状态到另一种状态**使用逐步非线性缓动**，提供冷静和自然运动。

- 如果可能，请 **在悬停时使用细小动画** 来指示鼠标下的交互式元素。

- 如果非常依赖于功能中的动画，则 **可提供一种方法，用于** 将所有) 功能从本地 (> "工具" " **选项** " 对话框中的选项。

- **一次只能出现一次动画** 并只传达一条信息。 移动或尝试传达多个对象的多个对象可能会造成混淆。

- **个很微妙非常重要。** 在大多数情况下，动画不需要用户注意来提供其目的。 计时、排序和行为方面的细微变化可能会显著影响感知，并可以在有效和低效动画之间产生差别。

- 当使用动画吸引事情时，请 **确保有必要中断用户**的想法训练。

- 通过动画**显示进度或状态时**：

  - 当基础进程不前进时，停止显示进度移动。

  - 将不确定的进程与确定性进程区分开来。

  - 确保动画具有可识别的完成和失败状态。

  - 最大程度地减少使用效果动画，这些动画显示状态，并通过提供实际使用的附加信息确保它们具有真正的价值。 示例包括暂时性状态更改和突发情况

#### <a name="animation-donts"></a>动画不应：

- 不要使用少量移动 (在小) 空间内移动。 更喜欢在移动对象上淡化和更改。

- 不要使用在大范围屏幕房地产上发生的动画。 无论大小如何，这种形式的动画都将分散给用户。

- 不要使用与用户当前所焦点的对象相关的动画或与之交互的对象。

- 不要使用需要用户交互来重置状态的动画，如强制用户响应闪烁的通知，使其停止闪烁。 以任何方式与它们进行交互应该足以消除它们。

有关这些最佳实践的应用程序的详细信息，请参阅 [动画模式](../../extensibility/ux-guidelines/animations-for-visual-studio.md#BKMK_AnimationPatterns)。

### <a name="animation-metrics"></a>动画指标

- 系统在不到10毫秒的时间内应对用户手势做出反应。

- 动画转换的完成时间不应超过500毫秒。

- 补偿需要更长时间的转换的一种方法是将其分为两部分。 例如，动画的第一部分可以是空的内容容器 (最多500毫秒) ，然后将内容淡入容器 (最多500毫秒) 。

- 对于可以计算的加载时间，首选的进度指示器 (按百分比完成进度指示器) 。

- 对于无法计算的加载时间， (加载或工作指示器) 等繁忙指示器，如光标或嵌入的旋转动画。

### <a name="animation-as-communicator"></a>作为 communicator 的动画
在 Visual Studio UI 中，动画仅用作一种通信工具。  它用于传达各种信息，如 UI 中的结构更改 (例如，当菜单打开或关闭) 时。 动画可帮助直观显示复杂系统的时间相关行为，如安装进度可视化。 还可以使用动画来吸引警报和通知。

 UI 动画的工作方式通常有四种：可视化、吸引注意、模拟和响应时间/进度指示器。

#### <a name="visualize"></a>可视化
动画可以强调对象的三维性质，并使用户可以更轻松地可视化其空间结构。 若要实现此目的，动画可能需要以一个完整的圆旋转对象，慢慢地来回翻转，或将对象置于更近的点，稍微增加其大小以强调滚动更新或焦点。

尽管可以使用用户控件移动三维对象，但设计人员应提前 (以编程方式或手动方式确定) 如何最好地对实现对象的最佳理解进行动画处理。 然后，用户可以通过将光标置于对象上来激活此编程动画，而用户控制的移动要求用户了解如何操作对象。 将移动限制为单个轴或一次方向，缩放、旋转或转换，但不要同时执行多个操作。

"可视化" 类别包括数据、关系、状态、结构、序列和时间方面的内容。

##### <a name="data"></a>数据
阐释复杂和可变信息：

- 在信息可视化中移动，如图表和图形

- 逐步完成序列、指导教程和分页

- 调用详细信息、指向和突出显示特定信息

- 覆盖重点元素顶部的详细信息和其他信息

- 从一种结构或组织表示形式变形

- 使用时间滑块、角拐和往复式滑轨以及传输控制 (播放、停止和暂停) 表示一段时间内的更改

##### <a name="relationships"></a>关系

- 阐释项彼此之间的关系或与给定项相关的项

- 显示层次结构、父子关系或同级关系

- 一个元素生成另一个元素

- 一个元素减至另一个元素

- 受限一个元素

##### <a name="state"></a>状态

- 内容更新

- 用户焦点和选择

- 进度

- 错误

##### <a name="structure"></a>结构

- 在一个节点上透视结构

- 通常

- 最小化和最大化，或者展开和折叠

##### <a name="sequence"></a>序列

- 幻灯片放映序列

- 翻转图片

##### <a name="time"></a>时间

- 显示随时间、时间间隔和 screencast 变化的更改

- 移动到垃圾桶、undo 和 redo

- 还原历史记录状态

#### <a name="attract-attention"></a>吸引关注
如果目标是将用户的注意力绘制到多个元素之外的一个元素中，或者为了提醒用户更新信息，则可以使用动画。 例如，应用程序起始页可能会使用入门按钮，该按钮在页面加载后将滑入到位。

通常，屏幕上的最后一个移动元素会 attracts 用户的注意力。  在一系列经过动画处理的元素中，用户注意将跟随最后一个移动对象。

##### <a name="alert"></a>警报

- 提醒用户，注意并显示进度

- 显示某个内容正在正确或不正确，或者显示进度或进度更改

- 在任务期间提示用户，例如联机查找详细信息或了解当前任务

##### <a name="notifications"></a>通知

- 提醒用户有关错误条件

- 中断用户以查看他们是否想要参加其他内容

- 轻轻向用户通知进程已完成或已更改，如下载完成时。

#### <a name="simulate"></a>Simulate
此类别涵盖 physicality 和维数。

- 说明对象来源或对象的目标位置

- 展开和折叠或打开和关闭

- 平移、滚动和翻页

- 堆叠和 z 顺序

- 轮播和折叠

- 翻转和旋转 UI

#### <a name="response-and-progress-indicators"></a>响应和进度指示器
进度指示器具有几个显著的优点：

- 确定性和不确定的进度指示器再次向用户，系统尚未崩溃并正在处理问题。

- 确定性指示器使用户能够了解该操作的进展情况，并使感觉更接近完成。

## <a name="animation-patterns"></a><a name="BKMK_AnimationPatterns"></a> 动画模式

### <a name="overview"></a>概述
Visual Studio 中的动画旨在提供特定的功能，而不会影响用户工作效率。 通常，Visual Studio 中的动画应为：

- 小型和非引人注目

- 自然和现实

- 微妙和温柔

- 快速高效

- 宽松，不十万火急

下图显示了我们建议用于 Visual Studio 的动画样式。 使用淡入/淡出的动画或细微动画是最常用的。 移动动画的应用程序（如展开和收缩、X 和 Y 位置更改和旋转）会受到限制。

![Visual Studio 的建议动画样式](../../extensibility/ux-guidelines/media/1202-a_vsanimstyles.png "1202-a_VSAnimStyles")<br />Visual Studio 的建议动画样式

#### <a name="appear-and-disappear"></a>显示并消失
使用此模式时，元素可以在无需过渡动画的情况下从可见切换到无视图切换。

![显示并消失动画](../../extensibility/ux-guidelines/media/1202-b_appearanddisappear.png "1202-b_AppearAndDisappear")<br />显示并消失动画

##### <a name="correct-usage"></a>正确使用
需要立即显示或消失的全新 UI 元素，以便用户既不分散也不会受到阻碍。 此外，转换速度缓慢的动画可能会被视为性能拖动，这不会出现在外观上并消失的样式。

##### <a name="incorrect-usage"></a>用法不正确
UI 出现的情况突然出现，用户不知道发生了什么情况，添加动画会有助于上下文理解。

##### <a name="animation-properties"></a>动画属性
时间延迟通常为零秒。

##### <a name="examples"></a>示例
- 自动隐藏工具窗口

- 键盘激活的编辑器 UI，如 IntelliSense 和参数帮助

- 展开和折叠代码区域

#### <a name="fade-in-and-fade-out"></a>淡入和淡出
使用此模式时，UI 元素将从不可见 (0% opacity) 转换为可见 (100% 不透明) ，反之亦然。

![淡入和淡出动画](../../extensibility/ux-guidelines/media/1202-c_fadeinfadeout.png "1202-c_FadeInFadeOut")<br />淡入和淡出动画

##### <a name="correct-usage"></a>正确使用
这是最常推荐的 UI 动画。 这是一种微妙的影响，它增加了不中断流的兴趣。 在某些情况下，用户甚至可能不会意识到有动画，觉察平滑和流动的 UI 系统。

##### <a name="animation-properties"></a>动画属性

- 开始不透明度：0% （对于淡入，100%）

- 结束不透明度：100% 的淡入，0% 表示淡出

- 持续时间：作为组合动画序列的一部分使用时，200毫秒独立，100毫秒

- 缓动样式：正弦 InOut

##### <a name="examples"></a>示例

- 自动隐藏工具窗口

- 菜单打开并关闭

- 背景和前景选项卡转换

#### <a name="color-blend-from-a-to-b"></a>从 A 到 B 的颜色混合
使用此模式时，UI 元素从颜色 A 变为颜色 B。

![颜色混合动画](../../extensibility/ux-guidelines/media/1202-d_colorblend.png "1202-d_ColorBlend")<br />颜色混合动画

##### <a name="correct-usage"></a>正确使用
当 UI 元素将颜色从一个上下文或状态更改为另一个时，转换为动态转换。

##### <a name="animation-properties"></a>动画属性

- 开始颜色： UI 特定

- 结束颜色： UI 特定

- 持续时间：作为组合动画序列的一部分使用时，200毫秒独立，100毫秒

- 缓动样式：正弦 InOut

##### <a name="examples"></a>示例

- 文档窗口状态转换 (活动、上次活动和非活动状态) 

- 工具窗口状态转换 (重点和失去焦点) 

#### <a name="expand-and-contract"></a>展开和收缩
使用此模式时，UI 元素以 X、Y 或双向方向展开。

![展开和收缩动画](../../extensibility/ux-guidelines/media/1202-e_expandcontract.png "1202-e_ExpandContract")<br />展开和收缩动画

##### <a name="correct-usage"></a>正确使用
当 UI 元素将大小从一个上下文更改到另一个上下文时，为动态转换。

##### <a name="animation-properties"></a>动画属性

- X 刻度：% 或特定的维度 (以像素为单位) 

- Y 刻度：% 或特定的维度 (（以像素为单位）) 

- 定位点位置：对于从右到左书写的语言，通常为左上角 () 或右上 () 

- 持续时间：作为组合动画序列的一部分使用时，200毫秒独立，100毫秒

##### <a name="examples"></a>示例

- 体系结构资源管理器面板展开和折叠

- Visual Studio 2017 开始页面项展开和折叠

#### <a name="x-y-position-change"></a>X Y 位置更改
使用此模式时，UI 元素将更改其 X 或 Y 位置，或同时更改两者。

![X Y 位置更改动画](../../extensibility/ux-guidelines/media/1202-f_xypositionchange.png "1202-f_XYPositionChange")<br />X Y 位置更改动画

##### <a name="correct-usage"></a>正确使用
当 UI 元素将位置从一个上下文更改到另一个上下文时，为动态转换。

##### <a name="animation-properties"></a>动画属性

- 开始 X 和 Y 位置： UI 特定

- 结束 X 和 Y 位置： UI 特定

- 运动路径：无

- 持续时间：作为组合动画序列的一部分使用时，200毫秒独立，100毫秒

- 缓动样式：正弦 InOut

##### <a name="example"></a>示例
选项卡重新排序

#### <a name="rotate"></a>旋转
通过此模式，UI 元素会旋转。

![UI 元素旋转动画](../../extensibility/ux-guidelines/media/1202-g_rotate.png "1202-g_Rotate")<br />UI 元素旋转动画

##### <a name="correct-usage"></a>正确使用
仅适用于不确定的旋转进度指示器。

##### <a name="animation-properties"></a>动画属性

- 旋转度：360

- 旋转中心：对象的中间

- 持续时间：连续

##### <a name="example"></a>示例
不确定的进度指示器 (旋转) 

### <a name="common-shell-ui-actions-and-recommended-animations"></a>常见 shell UI 操作和建议的动画

#### <a name="tab-open"></a>打开的选项卡
![选项卡打开动画](../../extensibility/ux-guidelines/media/1202-h_tabopen.png "1202-h_TabOpen")<br />选项卡打开动画

- 样式：显示

- 持续时间：0秒

#### <a name="tab-close"></a>制表符关闭
![选项卡关闭动画](../../extensibility/ux-guidelines/media/1202-i_tabclose.png "1202-i_TabClose")<br />选项卡关闭动画

- Style： X 位置更改

- 持续时间：200毫秒

#### <a name="tab-reorder"></a>选项卡重新排序
![Visual Studio 中的选项卡重新排序动画](../../extensibility/ux-guidelines/media/1202-j_tabreorder.png "1202-j_TabReorder")<br />选项卡重新排序动画

- Style： X 位置更改

- 持续时间：200毫秒

#### <a name="close-floating-document"></a>关闭浮动文档
![关闭浮动文档动画](../../extensibility/ux-guidelines/media/1202-k_closefloatingdocument.png "1202-k_CloseFloatingDocument")<br />关闭浮动文档动画

- 样式：显示

- 持续时间：200毫秒

#### <a name="window-state-transition"></a>窗口状态转换
![窗口状态转换动画](../../extensibility/ux-guidelines/media/1202-l_windowstatetransition.png "1202-l_WindowStateTransition")<br />窗口状态转换动画

- Style：若要与其他窗口保持一致，请让当前操作系统定义文档关闭动画。

- 持续时间：200毫秒

#### <a name="menu-open"></a>菜单打开
![菜单打开动画](../../extensibility/ux-guidelines/media/1202-m_menuopen.png "1202-m_MenuOpen")<br />菜单打开动画

- 样式：淡入

- 持续时间：200毫秒

#### <a name="menu-close"></a>菜单关闭
![菜单关闭动画](../../extensibility/ux-guidelines/media/1202-n_menuclose.png "1202-n_MenuClose")<br />菜单关闭动画

- 样式：淡出

- 持续时间：200毫秒

#### <a name="auto-hide-tool-window-reveal"></a>自动隐藏工具窗口显示
![自动隐藏工具窗口显示动画](../../extensibility/ux-guidelines/media/1202-o_autohidetoolwindowreveal.png "1202-o_AutoHideToolWindowReveal")<br />自动隐藏工具窗口显示动画

- 样式：显示

- 持续时间：0秒
